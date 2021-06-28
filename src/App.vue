<template>
  <div id="app">
    <div class="nav-btns">
      <a-menu v-model="current" mode="horizontal">
        <a-menu-item key="table">TableDemo</a-menu-item>
        <a-menu-item key="tree">TreeDemo</a-menu-item>
        <a-menu-item key="dataStatistics">DataStatistics</a-menu-item>
        <a-menu-item key="orderList">orderList</a-menu-item>
        <a-menu-item key="treeArea">treeArea</a-menu-item>
      </a-menu>
    </div>
    <TableDemo v-if="current[0] === 'table'"></TableDemo>
    <TreeDeom v-if="current[0] === 'tree'"></TreeDeom>
    <DataStatisticsPage
      v-if="current[0] === 'dataStatistics'"
    ></DataStatisticsPage>
    <OrderList v-if="current[0] === 'orderList'"></OrderList>
    <TreeArea v-if="current[0] === 'treeArea'"></TreeArea>
  </div>
</template>

<script>
import TableDemo from "./components/TableDemo";
import TreeDeom from "./components/TreeDemo";
import DataStatisticsPage from "./components/dataStatisticsPage";
import OrderList from "./components/orderList";
import TreeArea from "./components/TreeArea";
export default {
  name: "App",
  components: {
    TableDemo,
    TreeDeom,
    DataStatisticsPage,
    OrderList,
    TreeArea,
  },
  data() {
    return { current: ["treeArea"] };
  },
  methods: {},
};
</script>

<style lang="less">
#app {
  margin: 0;
  padding: 40px;
}
.nav-btns {
  text-align: center;
  margin-bottom: 20px;
}
</style>
