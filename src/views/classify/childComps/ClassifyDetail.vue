<!--
 * @Author: 孙秋云
 * @Date: 2020-06-21 17:04:44
 * @LastEditTime: 2021-05-09 19:38:43
 * @LastEditors: Please set LastEditors
 * @Description: 分类商品详情
 * @FilePath: \MiniSuper\src\views\classify\childComps\ClassifyDetail.vue
-->
<template>
  <div class="classify-detail">
    <classify-list :goods="showGoods" />
  </div>
</template>

<script>
import ClassifyList from "components/content/goods/ClassifyList";
import { getHomeGoods } from "network/home.js";
export default {
  components: {
    ClassifyList
  },
  computed: {
    showGoods() {
      return this.goods.pop.list;
    }
  },
  data() {
    return {
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      }
    };
  },
  created() {
    this.getHomeGoods("pop");
  },
  methods: {
    getHomeGoods(type) {
      //商品展示数据
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.data.list);
        this.goods[type].page += 1;
      });
    }
  }
};
</script>

<style scoped>
.classify-detail {
  height: 100%;
  display: flex;
}
</style>
