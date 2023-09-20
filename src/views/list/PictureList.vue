<template>
  <page-header-wrapper
    :tab-list="tabList"
    :tab-active-key="tabActiveKey"
    :tab-change="(key) => {
      this.tabActiveKey = key
    }"
    content="段落示意：  ant.design  。"
  >
    <template v-slot:extraContent>
      <div style="width: 155px; margin-top: -20px;"><img style="width: 100%" :src="extraImage"/></div>
    </template>
    <a-list
      rowKey="id"
      :grid="{gutter: 24, lg: 3, md: 2, sm: 1, xs: 1}"
      :dataSource="dataSource"
      class="picture-list"
    >
      <a-list-item slot="renderItem" slot-scope="item">
        <a-card :hoverable="true" size="small">
          <img
            slot="cover"
            alt="example"
            :src="item.image"
          />
          <a-card-meta>
            <a slot="title">{{ item.place }}</a>
            <!--              <a-avatar class="card-avatar" slot="avatar" :src="item.avatar" size="large"/>-->
            <div class="meta-content" slot="description">{{ item.content }}</div>

          </a-card-meta>
          <template class="ant-card-actions" slot="actions">
            <a>操作一</a>
            <a>操作二</a>
          </template>
        </a-card>
      </a-list-item>
    </a-list>
  </page-header-wrapper>
</template>

<script>

import axios from "axios";

// const dataSource = []
// for (let i = 0; i < 11; i++) {
//   dataSource.push({
//     id: i,
//     title: 'Alipay',
//     avatar: 'https://gw.alipayobjects.com/zos/rmsportal/WdGqmHpayyMjiEhcKoVE.png',
//     content: '在中台产品的研发过程中，会出现不同的设计规范和实现方式，但其中往往存在很多类似的页面和组件，这些类似的组件会被抽离成一套标准规范。',
//     image: 'https://ts1.cn.mm.bing.net/th?id=OIP-C.Zte3ljd4g6kqrWWyg-8fhAHaEo&w=316&h=197&c=8&rs=1&qlt=90&o=6&dpr=1.1&pid=3.1&rm=2',
//     place: '杭州 西湖 苏堤',
//     user: '王宝强',
//     date: '2023-09-13 21:26:01',
//   })
// }

export default {
  name: 'PictureList',
  data() {
    const dataSource = []
    this.tabList = [
      {key: 'tab1', tab: '快速开始'},
      {key: 'tab2', tab: '产品简介'},
      {key: 'tab3', tab: '产品文档'}
    ]
    return {
      tabActiveKey: 'tab1',

      extraImage: 'https://gw.alipayobjects.com/zos/rmsportal/RzwpdLnhmvDJToTdfDPe.png',
      dataSource
    }
  },
  methods: {
    testFun() {
      this.$message.info('快速开始被点击！')
    }
  },
  //mounted(): 初始化页面完成后 会自动执行， 调方法可以调methods里的方法
  mounted() {
    this.$nextTick(() => {
      this.testFun();
    });
    axios.get('https://v.api.aa1.cn/api/phone/guishu-api.php?phone=17857336866')
      .then(response => {
        console.log(response.data)
        this.dataSource = [response.data].map(item => {
          return {
            place: item.province,
            user: item.city,
            content: item.sp,
            image: 'https://ts1.cn.mm.bing.net/th?id=OIP-C.Zte3ljd4g6kqrWWyg-8fhAHaEo&w=316&h=197&c=8&rs=1&qlt=90&o=6&dpr=1.1&pid=3.1&rm=2',
          }
        });
      })
      .catch(error => {
        console.log(error);
      });
  }
}
</script>

<style lang="less" scoped>
@import "~@/components/index.less";

.picture-list {
  :deep(.ant-card-body:hover) {
    .ant-card-meta-title > a {
      color: @primary-color;
    }
  }

  :deep(.ant-card-meta-title) {
    margin-bottom: 12px;

    & > a {
      display: inline-block;
      max-width: 100%;
      color: rgba(0, 0, 0, .85);
    }
  }

  :deep(.meta-content) {
    position: relative;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    height: 64px;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;

    margin-bottom: 1em;
  }
}

.card-avatar {
  width: 48px;
  height: 48px;
  border-radius: 48px;
}

.ant-card-actions {
  background: #f7f9fa;

  li {
    float: left;
    text-align: center;
    margin: 12px 0;
    color: rgba(0, 0, 0, 0.45);
    width: 50%;

    &:not(:last-child) {
      border-right: 1px solid #e8e8e8;
    }

    a {
      color: rgba(0, 0, 0, .45);
      line-height: 22px;
      display: inline-block;
      width: 100%;

      &:hover {
        color: @primary-color;
      }
    }
  }
}

.new-btn {
  background-color: #fff;
  border-radius: 2px;
  width: 100%;
  height: 188px;
}

</style>
