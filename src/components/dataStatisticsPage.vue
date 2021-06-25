<template>
  <div>
    <a-card>
      <a-row>
        <a-col span="8">
          <div>
            <span class="siyu-size">今日数据</span>
            <span class="siyu-newtime">更新时间: 2021-06-04 16:54:09</span>
            <a-icon class="siyu-eye" v-if="eye" type="eye" @click="handleEye" />
            <a-icon
              class="siyu-eye"
              v-if="!eye"
              type="eye-invisible"
              @click="handleCoseEye"
            />
          </div>
        </a-col>
        <a-col span="1" :offset="15">
          <a class="siyu-eye" @click="handleEdit">编辑</a>
        </a-col>
      </a-row>
      <div class="siyu-main">
        <a-row>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                实际收款金额(元)
                <a-tooltip
                  title="1.订单完成时间在统计时间内，现金类收款的金额总和，统计时减去现金类退款的金额；
                         2.现金类包含：现金、微信、支付宝、刷卡、E卡、自定义记账方式。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0.00</p>
              <p>
                昨日
                <span class="siyu-num">0.00</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                实际退款金额(元)
                <a-tooltip
                  title="退款时间在统计时间内，通过现金类方式退款的金额"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0.00</p>
              <p>
                昨日
                <span class="siyu-num">0.00</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                实际消耗金额(元)
                <a-tooltip
                  title="1.订单完成时间在统计时间内，客户消耗类收款的金额总和，统计时减去客户消耗类退款的金额；
                        2.客户消耗类包含：客户余额/权益次数消耗，不包括余额购买次卡/定制卡的消耗，其中权益次数消耗取折算后的单次金额计算客户消耗金额。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0.00</p>
              <p>
                昨日
                <span class="siyu-num">0.00</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                实消耗退款金额(元)
                <a-tooltip
                  title="退款时间在统计时间内，产生会员消耗类回退的金额，不包括余额购买次卡/定制卡的消耗退款。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0.00</p>
              <p>
                昨日
                <span class="siyu-num">0.00</span>
              </p>
            </div>
          </a-col>
        </a-row>
        <a-row>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                成交客户数
                <a-tooltip
                  title="1.订单完成时间在统计时间内，付款的客户数；
                      2.散客订单按订单数统计，同一客户去重按1统计"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0</p>
              <p>
                昨日
                <span class="siyu-num">0</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                客单价(元)
                <a-tooltip
                  title="1.即消费客单价，不包括开卡充值的数据；
                         2.订单完成时间在统计时间内，品项订单成交金额/品项订单成交客户数。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0.00</p>
              <p>
                昨日
                <span class="siyu-num">0.00</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                新增会员数
                <a-tooltip
                  title="1.即消费客单价，不包括开卡充值的数据；
                         2.订单完成时间在统计时间内，品项订单成交金额/品项订单成交客户数。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0</p>
              <p>
                昨日
                <span class="siyu-num">0</span>
              </p>
            </div>
          </a-col>
          <a-col span="6">
            <div>
              <p class="siyu-color">
                开卡充值数
                <a-tooltip
                  title="1.订单完成时间在统计时间内，开卡（次卡、折扣卡、组合卡）或充值（充值卡、充值）的客户数；2.同一客户去重按1统计。"
                >
                  <a-icon type="question-circle-o" class="icon" />
                </a-tooltip>
              </p>
              <p class="siyu-size">0</p>
              <p>
                昨日
                <span class="siyu-num">0</span>
              </p>
            </div>
          </a-col>
        </a-row>
      </div>
    </a-card>
    <!-- 编辑弹框 -->
    <div class="siyu-modal" ref="modal">
      <a-modal
        v-model="visible"
        title="自定义数据"
        @ok="handleOk"
        :getContainer="() => $refs.modal"
        width="700px"
      >
        <a-row>
          <a-col span="5">已选数据类型:</a-col>
          <a-col span="19">
            <a-tag
              closable
              class="siyu-tag"
              v-for="(item, index) in selectTags"
              :key="item.key"
              @close="onCloseTag(index)"
              >{{ item.datatype || item.dataname }}</a-tag
            >

            <!-- <a-tag closable class="siyu-tag">实际收款金额(元)</a-tag>
            <a-tag closable class="siyu-tag">实际消耗金额(元)</a-tag>
            <a-tag closable class="siyu-tag">实际退款金额(元)</a-tag>
            <a-tag closable class="siyu-tag">实消耗退款金额(元)</a-tag>
            <a-tag closable class="siyu-tag">服务销售金额(元)</a-tag>
            <a-tag closable class="siyu-tag">产品销售金额(元)</a-tag>
            <a-tag closable class="siyu-tag">开卡充值金额(元)</a-tag>
            <a-tag closable class="siyu-tag">PLUS会员销售(元)</a-tag>
            <a-tag closable class="siyu-tag">成交客户数</a-tag>
            <a-tag closable class="siyu-tag">客单价(元)</a-tag>
            <a-tag closable class="siyu-tag">新增会员数</a-tag>
            <a-tag closable class="siyu-tag">开卡充值数</a-tag>-->
          </a-col>
        </a-row>

        <a-row class="siyu-rowbutton">
          <a-alert message="数据最多可选择8个" type="info" show-icon />
        </a-row>
        <!-- 弹框表格 -->
        <a-table
          :row-selection="rowSelection"
          :columns="columns"
          :data-source="data"
          :scroll="{ y: 300 }"
          :pagination="false"
          rowKey="key"
        ></a-table>
      </a-modal>
    </div>
  </div>
</template>
<script>
const defaultKeys = [1, 2, 3, 4, 5, 6, 7, 8];
const data = [
  {
    key: 1,
    dataname: "实际收款金额(元)",
    disabled: false,
    datadescription:
      "1.订单完成时间在统计时间内，现金类收款的金额总和，统计时减去现金类退款的金额;2.现金类包含：现金、微信、支付宝、刷卡、E卡、自定义记账方式。",
  },
  {
    key: 2,
    dataname: "实际消耗金额(元)",
    disabled: false,
    datadescription: "退款时间在统计时间内，通过现金类方式退款的金额",
  },
  {
    key: 3,
    dataname: "实际退款金额(元)",
    disabled: false,
    datadescription:
      "1.订单完成时间在统计时间内，客户消耗类收款的金额总和，统计时减去客户消耗类退款的金额；2.客户消耗类包含：客户余额/权益次数消耗，不包括余额购买次卡/定制卡的消耗，其中权益次数消耗取折算后的单次金额计算客户消耗金额。",
  },
  {
    key: 4,
    dataname: "实消耗退款金额(元)",
    disabled: false,
    datadescription:
      "退款时间在统计时间内，产生会员消耗类回退的金额，不包括余额购买次卡/定制卡的消耗退款。",
  },
  {
    key: 5,
    datatype: "交易数据",
    disabled: false,
    dataname: "服务销售金额(元)",
    datadescription:
      "1.订单完成时间在统计时间内，客户消费服务项目的(实际付款金额+客户消耗金额)之和，统计时减去服务的实际退款金额及客户消耗回退金额；2.服务的客户消耗金额去除赠送服务权益的消耗；3.一个品项订单若包含了服务和产品，统计时仅统计服务的金额",
  },
  {
    key: 6,
    datatype: "交易数据",
    disabled: false,
    dataname: "产品销售金额(元)",
    datadescription:
      "1.订单完成时间在统计时间内，客户购买产品的(实际收款金额+客户消耗金额)之和，统计时减去产品的实际退款金额及客户消耗回退金额；2.一个品项订单若包含了服务和产品，统计时仅统计产品的金额",
  },
  {
    key: 7,
    datatype: "交易数据",
    disabled: false,
    dataname: "开卡充值金额(元)",
    datadescription:
      "1.订单完成时间在统计时间内，开卡（充值卡、次卡、定制卡、折扣卡)或充值的实际收款金额总和，统计时减去开卡充值实际退款的金额；2.消耗会员余额进行开卡的金额不计入开卡充值金额。",
  },
  {
    key: 8,
    datatype: "交易数据",
    disabled: false,
    dataname: "PLUS会员销售金额(元)",
    datadescription: "订单完成时间在统计时间内，客户购买PLUS会员的金额之和。",
  },
  {
    key: 9,
    datatype: "客户数据",
    disabled: false,
    dataname: "成交客户数",
    datadescription:
      "1.订单完成时间在统计时间内，付款的客户数；2.散客订单按订单数统计，同一客户去重按1统计",
  },
  {
    key: 10,
    datatype: "客户数据",
    dataname: " 客单价(元)",
    disabled: false,
    datadescription:
      "1.即消费客单价，不包括开卡充值的数据；2.订单完成时间在统计时间内，品项订单成交金额/品项订单成交客户数。",
  },
  {
    key: 11,
    datatype: "客户数据",
    dataname: "新增会员数",
    disabled: false,
    datadescription:
      "1.即消费客单价，不包括开卡充值的数据；2.订单完成时间在统计时间内，品项订单成交金额/品项订单成交客户数。",
  },
  {
    key: 12,
    datatype: "客户数据",
    dataname: "开卡充值数",
    disabled: false,
    datadescription:
      "1.订单完成时间在统计时间内，开卡（次卡、折扣卡、组合卡）或充值（充值卡、充值）的客户数；2.同一客户去重按1统计。",
  },
];
export default {
  name: "dataStatisticsPage",
  data() {
    return {
      eye: true,
      visible: false,
      columns: [
        {
          title: "数据类型",
          dataIndex: "datatype",
          key: "datatype",
          width: 100,
        },

        {
          title: "数据名称",
          dataIndex: "dataname",
          key: "dataname",
          width: 100,
        },
        {
          title: "数据描述",
          dataIndex: "datadescription",
          key: "datadescription",
        },
      ],
      data,
      // defaultKeys: [1, 2, 3, 4, 5, 6, 7, 8],
      defaultKeys: defaultKeys,
      selectTags: [],
    };
  },
  methods: {
    handleEye() {
      this.eye = false;
    },
    handleCoseEye() {
      this.eye = true;
    },
    // 编辑对话框显示与隐藏
    handleEdit() {
      this.visible = true;
    },
    handleOk(e) {
      console.log(e);
      this.visible = false;
    },
    onChangeTable(rowKeys) {
      this.defaultKeys = rowKeys;
      this.initTags();
      this.data.forEach((item) => {
        item.disabled = rowKeys.indexOf(item.key) == -1 && rowKeys.length >= 8;
      });
      this.data = [...this.data];
    },
    initTags() {
      this.selectTags = this.data.filter(
        (item) => this.defaultKeys.indexOf(item.key) !== -1
      );
    },
    onCloseTag(index) {
      this.selectTags.splice(index, 1);
      let selectedKeys = [];
      this.selectTags.forEach((item) => {
        selectedKeys = selectedKeys.concat(item.key);
      });
      this.defaultKeys = selectedKeys;
      this.onChangeTable(selectedKeys);
    },
  },
  computed: {
    rowSelection() {
      return {
        columnTitle: "选择", // 去掉头部全选框
        hideDefaultSelections: true,
        selectedRowKeys: this.defaultKeys, // 默认选中
        onChange: (selectedRowKeys) => {
          selectedRowKeys = Array.from(new Set(selectedRowKeys));
          this.onChangeTable(selectedRowKeys);
        },
        getCheckboxProps: (record) => {
          return {
            props: {
              disabled: record.disabled,
            },
          };
        },
      };
    },
  },
  created() {
    // 调接口，判断
    // 1.有值； this.defaultKeys = res.data;
    // 2.没有值：this.defaultKeys = defaultKeys;
    this.onChangeTable(this.defaultKeys);
  },
};
</script>
<style scoped>
.siyu-main {
  padding: 25px 15px;
}
.siyu-size {
  font-size: 20px;
  color: #323232;
  margin-bottom: 0;
}
.siyu-color {
  color: #969799;
}
.siyu-borber {
  border-left: 1px solid #969799;
  padding-left: 70px;
}
.siyu-newtime {
  padding: 0 15px;
}
.siyu-eye {
  font-size: 16px;
}
.siyu-num {
  margin-left: 10px;
}
.siyu-choose {
  margin: 0 5px;
}
.siyu-tag {
  margin-bottom: 3px;
}
.siyu-rowbutton {
  margin-top: 10px;
  margin-bottom: 8px;
}
</style>
