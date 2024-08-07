<template>
  <view class="container">
    <view class="input-group">
      <text class="label">楼上电量比例:</text>
      <input
        type="text"
        v-model.number="upstairsRatio"
        placeholder="请输入楼上电量比例"
        class="input"
      />
    </view>
    <view class="input-group">
      <text class="label">楼下电量比例:</text>
      <input
        type="text"
        v-model.number="downstairsRatio"
        placeholder="请输入楼下电量比例"
        class="input"
      />
    </view>
    <view class="input-group">
      <text class="label">总使用电量:</text>
      <input
        type="text"
        v-model.number="totalElectricity"
        placeholder="请输入总使用电量"
        class="input"
      />
    </view>
    <view class="input-group">
      <text class="label">本人电量比例:</text>
      <input
        type="text"
        v-model.number="myRatio"
        placeholder="请输入本人电量比例"
        class="input"
      />
    </view>
    <view class="input-group">
      <text class="label">当月缴费:</text>
      <input
        type="text"
        v-model.number="monthlyPayment"
        placeholder="请输入当月缴费"
        class="input"
      />
    </view>
    <view class="input-group">
      <text class="label">单价:</text>
      <text class="fixed-value">{{ pricePerUnit }} 元</text>
    </view>
    <view class="input-group">
      <button class="calculate-button" @click="calculateCost">计算</button>
    </view>
    <view class="result-group" v-if="calculated">
      <text class="result-label">结果: </text>
      <text class="result">{{ result.toFixed(2) }} 元</text>
    </view>
  </view>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class Index extends Vue {
  upstairsRatio: number = 0;
  downstairsRatio: number = 0;
  totalElectricity: number = 0;
  myRatio: number = 0;
  monthlyPayment: number = 0;
  pricePerUnit: number = 0.85;
  calculated: boolean = false;
  result: number = 0;

  calculateCost() {
    const totalRatio = this.upstairsRatio + this.downstairsRatio;
    if (totalRatio === 0) {
      this.result = 0;
    } else {
      const myCost =
        (this.totalElectricity / totalRatio) * this.myRatio * this.pricePerUnit;
      this.result = this.monthlyPayment - myCost;
    }
    this.calculated = true;
  }
}
</script>

<style scoped>
.container {
  padding: 16px;
  max-width: 600px;
  margin: 0 auto;
  background-color: #f9f9f9;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}
.input-group,
.result-group {
  margin-bottom: 20px;
}
.label {
  display: block;
  margin-bottom: 5px;
  font-size: 16px;
  color: #333;
}
.input {
  width: 100%;
  padding: 8px; /* 调整padding */
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
  height: 40px;
  line-height: 1.5; /* 调整行高 */
}
.fixed-value {
  width: 100%;
  padding: 8px; /* 调整padding */
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
  height: 40px;
  line-height: 1.5; /* 调整行高 */
  background-color: #f0f0f0;
  color: #333;
}
.calculate-button {
  width: 100%;
  padding: 15px;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  box-sizing: border-box;
}
.calculate-button:hover {
  background-color: #0056b3;
}
.result-group {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
.result-label {
  font-size: 16px;
  color: #333;
}
.result {
  font-size: 16px;
  color: #007bff;
}

</style>
