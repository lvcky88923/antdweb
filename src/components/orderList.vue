<template>
  <div class="order-list">
    <a-tabs type="card" @change="callback">
      <a-tab-pane v-for="item in tabsList" :key="item.key" :tab="item.label">
        <a-table
          class="table-header"
          :columns="columns"
          :data-source="[]"
        ></a-table>
        <div class="table-lists" v-if="item.key == 1">
          <div class="table-item" v-for="item in 4" :key="item">
            <div class="table-header">
              <div class="order-info">
                <span>下单时间：2021-06-11 15:04:17</span>
                <span>低昂单编号：M1111111111111113</span>
                <span>品项/网店</span>
              </div>
              <div class="order-tags">
                <span>订单详情</span>
                -
                <span>备注</span>
              </div>
            </div>
            <a-table
              :columns="columns"
              :data-source="data"
              :showHeader="false"
              bordered
              :pagination="false"
              :rowClassName="rowClassName"
            ></a-table>
          </div>
        </div>
      </a-tab-pane>
    </a-tabs>
  </div>
</template>

<script>
const columns = [
  {
    title: "商品",
    dataIndex: "shop",
    key: "shop",
    width: "200px",
  },
  {
    title: "单价",
    dataIndex: "unitPrice",
    key: "unitPrice",
    width: "11%",
    align: "center",
  },
  {
    title: "数量",
    dataIndex: "number",
    key: "number",
    width: "7%",
    align: "center",
  },
  {
    title: "手艺人/销售",
    key: "craftsman",
    dataIndex: "craftsman",
    width: "12%",
    align: "center",
  },
  {
    title: "客户",
    dataIndex: "customer",
    key: "customer",
    width: "13%",
    align: "center",
  },
  {
    title: "金额",
    dataIndex: "amountMoney",
    key: "amountMoney",
    width: "10%",
    align: "center",
  },
  {
    title: "下单门店",
    dataIndex: "store",
    key: "store",
    width: "10%",
    align: "center",
  },
  {
    title: "状态",
    dataIndex: "status",
    key: "status",
    width: "75px",
    align: "center",
  },
  {
    title: "操作",
    dataIndex: "operation",
    key: "operation",
    width: "75px",
    align: "center",
  },
];

const data = [
  {
    key: "1",
    shop: "1w2",
    unitPrice: "32",
    number: "12",
    craftsman: "12332",
    customer: "12332",
    amountMoney: "12332",
    store: "12332",
    status: "status",
    operation: "12332",
  },
];

export default {
  data() {
    return {
      tabsList: [
        {
          key: "1",
          label: "全部",
        },
        {
          key: "2",
          label: "待付款",
        },
        {
          key: "3",
          label: "待发货",
        },
        {
          key: "4",
          label: "已发货",
        },
        {
          key: "5",
          label: "待到店消费",
        },
        {
          key: "6",
          label: "已完成",
        },
        {
          key: "7",
          label: "已取消",
        },
      ],
      data,
      columns,
    };
  },
  methods: {
    callback(key) {
      console.log(key);
    },
    rowClassName() {
      return "table-back";
    },
  },
};
</script>

<style lang="less" scoped>
.order-list {
  .table-header {
    /deep/ .ant-table-placeholder {
      display: none;
    }
  }
  .table-lists {
    margin-top: 20px;
    .table-item {
      &:not(:last-child) {
        margin-bottom: 20px;
      }
      .table-header {
        display: flex;
        justify-content: space-between;
        background-color: #f7f8fa;
        padding: 0 16px;
        line-height: 40px;
      }
      .order-info {
        color: #111;
        span {
          &:not(:first-child) {
            color: #969799;
            margin-left: 34px;
          }
        }
      }
      .order-tags {
        color: #8558fa;
        span {
          cursor: pointer;
        }
      }
      // /deep/.table-back {
      // background-color: #fafafa;
      // }
    }
  }
}
</style>
