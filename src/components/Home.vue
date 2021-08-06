<template>
  <div class="home">
    <home-header></home-header>
    <div class="home-main">
      <transition-group enter-active-class="slideInRight">
        <ul class="goods animated" :key="animatedCurrentKey">
          <li
            v-for="item in goods"
            class="one-com"
            v-show="isCurrent(item.kind)"
          >
            <one-commodity
              :itemId="item.id"
              :imgUrl="item.img"
              :title="item.title"
              :content="item.content"
              :price="item.price"
              :count="0"
            ></one-commodity>
          </li>
        </ul>
        <div :key="'0' + animatedCurrentKey">
          <p class="no-more-goods">没有更多商品啦，敬请期待!!!</p>
        </div>
      </transition-group>
    </div>

    <el-dialog title="提示" :visible.sync="dialogVisible" width="30%">
      <p>这是手机端应用，请用手机微信，或浏览器扫码打开</p>
      <img src="../../static/url.png" height="280" width="280" />
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false"
          >确 定</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
import OneCommodity from "./HomeOneCommodity.vue";
import HomeHeader from "./HomeHeader.vue";

export default {
  name: "home",
  data() {
    var UA = navigator.userAgent;
    var ipad = !!UA.match(/(iPad).*OS\s([\d_]+)/),
      isIphone = !!(!ipad && UA.match(/(iPhone\sOS)\s([\d_]+)/)),
      isAndroid = !!UA.match(/(Android)\s+([\d.]+)/),
      isPC = !(isIphone || isAndroid || ipad);
    return {
      goods: [
        {
          id: 1,
          kind: 1,
          img: "./static/imgs/goods/水果.png",
          title: "这是水果1",
          content: "这是水果介绍",
          price: 18,
        },
        {
          id: 2,
          kind: 1,
          img: "./static/imgs/goods/水果2.png",
          title: "这是水果2",
          content: "这是水果介绍",
          price: 20,
        },
        {
          id: 3,
          kind: 2,
          img: "./static/imgs/goods/蔬菜.png",
          title: "这是蔬菜1",
          content: "这是蔬菜介绍",
          price: 20,
        },
        {
          id: 4,
          kind: 2,
          img: "./static/imgs/goods/蔬菜2.png",
          title: "这是蔬菜2",
          content: "这是蔬菜介绍",
          price: 30,
        },
        {
          id: 5,
          kind: 3,
          img: "./static/imgs/goods/肉蛋.png",
          title: "这是肉蛋1",
          content: "这是肉蛋介绍",
          price: 10,
        },
        {
          id: 6,
          kind: 3,
          img: "./static/imgs/goods/肉蛋2.png",
          title: "这是肉蛋2",
          content: "这是肉蛋介绍",
          price: 15,
        },
        {
          id: 7,
          kind: 4,
          img: "./static/imgs/goods/速冻.png",
          title: "这是速冻1",
          content: "这是速冻介绍",
          price: 50,
        },
        {
          id: 8,
          kind: 4,
          img: "./static/imgs/goods/速冻2.png",
          title: "这是速冻2",
          content: "这是速冻介绍",
          price: 60,
        },
        {
          id: 9,
          kind: 5,
          img: "./static/imgs/goods/酒饮.png",
          title: "这是酒饮1",
          content: "这是酒饮介绍",
          price: 100,
        },
        {
          id: 10,
          kind: 5,
          img: "./static/imgs/goods/酒饮2.png",
          title: "这是酒饮2",
          content: "这是酒饮介绍",
          price: 70,
        },
        {
          id: 11,
          kind: 6,
          img: "./static/imgs/goods/乳品.png",
          title: "这是乳品1",
          content: "这是乳品介绍",
          price: 55,
        },
        {
          id: 12,
          kind: 6,
          img: "./static/imgs/goods/乳品2.png",
          title: "这是乳品2",
          content: "这是乳品介绍",
          price: 33,
        },
        {
          id: 13,
          kind: 7,
          img: "./static/imgs/goods/零食.png",
          title: "这是零食1",
          content: "这是零食介绍",
          price: 5,
        },
        {
          id: 14,
          kind: 7,
          img: "./static/imgs/goods/零食2.png",
          title: "这是零食2",
          content: "这是零食介绍",
          price: 15,
        },
      ],
      dialogVisible: isPC,
    };
  },
  computed: {
    animatedCurrentKey() {
      return this.$store.state.GoodsCurrentSelKind;
    },
  },
  methods: {
    //分类按钮点击时
    isCurrent(itemKind) {
      let currentKind = this.$store.state.GoodsCurrentSelKind;
      if (currentKind === 0) {
        //0表示全部商品
        return true;
      } else {
        return itemKind === currentKind;
      }
    },
  },
  components: {
    OneCommodity: OneCommodity,
    HomeHeader: HomeHeader,
  },
  //本地测试：http://localhost:8080/static/data/goods.json
  //gitHub：/shoppingApp/static/data/github-goods.json
  //阿里云：
  // mounted() {
  //   this.axios
  //     .get(
  //       "https://github.com/buzhengjingdewagnzi/shoppingApp-server/blob/main/static/data/goods.json"
  //     )
  //     .then((res) => {
  //       console.log(res)
  //       this.goods = [...res.data];
  //     })
  //     .catch(() => {
  //       this.axios.get("/static/data/goods.json").then((res) => {
  //         this.goods = [...res.data];
  //       });
  //     });
  // },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/variable.scss";

.home {
  width: 100%;
  padding-bottom: $NavHeight + 5px;
  padding-top: $HomeHeaderHeight;
}
.home-main {
  width: 100%;
  overflow-x: hidden;
}
.goods {
  width: 100%;
  list-style: none;
  padding: 0;
}
.goods > li {
  width: 100%;
}
.no-more-goods {
  height: 40px;
  line-height: 40px;
}
.slideInRight {
  animation-duration: 0.25s;
}
</style>
