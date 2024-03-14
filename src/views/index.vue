<template>
  <div id="index">
    <dv-full-screen-container class="bg">
      <dv-loading v-if="loading">Loading...</dv-loading>
      <!--     最外层-->
      <div v-else class="host-body">

        <div class="d-flex jc-center">
          <dv-decoration-10 style="width:33.3%;height:.0625rem;" />
          <div class="d-flex jc-center">
            <dv-decoration-8 :color="['#568aea', '#000000']" style="width:2.5rem;height:.625rem;" />
            <div class="title">
              <span class="title-text">风电功率预测系统</span>
              <dv-decoration-6 class="title-bototm" :reverse="true" :color="['#50e3c2', '#67a1e5']"
                style="width:3.125rem;height:.1rem;" />
            </div>
            <dv-decoration-8 :reverse="true" :color="['#568aea', '#000000']" style="width:2.5rem;height:.625rem;" />
          </div>
          <dv-decoration-10 style="width:33.3%;height:.0625rem; transform: rotateY(180deg);" />
        </div>

        <!-- 标题选项层-->
        <div class="d-flex jc-between px-2">
          <div class="d-flex" style="width: 40%">
            <div class="react-right ml-4" style="width: 6.25rem; text-align: left;background-color: #0f1325;"
              @click="currentTab = 0" :class="{ 'active': currentTab === 0 }">
              <span class="react-before"></span>
              <span class="text fw-b" style="margin-left: 70px;">风机展示</span>
            </div>
            <div class="react-right ml-3" style="background-color: #0f1325;" @click="currentTab = 1"
              :class="{ 'active': currentTab === 1 }">
              <span class="text fw-b">模型训练与长期预测</span>
            </div>
          </div>
          <div style="width: 40%" class="d-flex">
            <div class="react-left  mr-3 " style="background-color: #0f1325;" @click="currentTab = 2"
              :class="{ 'active': currentTab === 2 }">
              <span class="text fw-b">短期预测</span>
            </div>
            <div class="react-left mr-4" @click="currentTab = 3" :class="{ 'active': currentTab === 3 }"
              style="width: 6.25rem; background-color: #0f1325; text-align: right;">
              <span class="react-after"></span>
              <span class="text">{{ currentDateTime }}</span>
            </div>
          </div>
        </div>
        <!-- 身体部分1-->
        <div class="body-box" v-if="currentTab === 0">
          <!-- 第三行数据 -->
          <div class="content-box">
            <!-- <div>
              <dv-border-box-12>
                <centerLeft1 />
              </dv-border-box-12>
            </div> -->
            <div class="LeftBottom">
              <dv-border-box-12>
                <centerLeft4 @changeTab="handleTabChange" />
              </dv-border-box-12>
              <dv-border-box-13>
                <bottomLeft />
              </dv-border-box-13>

            </div>
            <div>
              <dv-border-box-13>
                <centerRight3 />
              </dv-border-box-13>
            </div>
          </div>

          <!-- 第四行数据 -->
          <!-- <div class="bototm-box">
            <dv-border-box-13>
              <bottomLeft />
            </dv-border-box-13>

          </div> -->
        </div>
        <!-- 身体部分2-->
        <div class="body-box" v-if="currentTab === 1">
          <!-- 身体部分3-->
          <!-- 第四行数据 -->
          <div class="bototm-box2">
            <dv-border-box-13>
              <secondCenter />
            </dv-border-box-13>

          </div>
        </div>
        <div class="body-box" v-if="currentTab === 2">
          <div class="bototm-box2">
            <dv-border-box-13>
              <ThreeCenter />
            </dv-border-box-13>

          </div>
        </div>


        <div class="body-box" v-if="currentTab === 3">
          <div>das</div>
          <fjdialog />
        </div>

      </div>
    </dv-full-screen-container>
  </div>
</template>

<script>
// import centerLeft1 from "./centerLeft1";
// import centerLeft2 from "./centerLeft2";
// import centerLeft3 from "./centerLeft3";
import centerLeft4 from "./centerLeft4";
// import centerRight1 from "./centerRight1";
// import centerRight2 from "./centerRight2";
import centerRight3 from "./centerRight3";
// import center from "./center";
// import bottomLeft from "./bottomLeft";
import secondCenter from "./secondCenter";
import ThreeCenter from "./ThreeCenter";
// import bottomLeft2 from "./bottomLeft2";
// import Fengji from '../components/echart/centerLeft2/fengji.vue';
// import Center from './center.vue';
// import fengji2 from "../components/echart/centerLeft2/fengji2.vue";
import fjdialog from "../components/dialog/dialog.vue";
export default {
  data() {
    return {
      loading: true,
      currentDateTime: "",
      currentTab: 0,
    };
  },
  components: {
    ThreeCenter,
    // centerLeft1,
    // centerLeft2,
    // centerLeft3,
    centerLeft4,
    // centerRight1,
    // centerRight2,
    centerRight3,
    // center,
    // bottomLeft,
    secondCenter,
    // Center,
    // fengji2,

    // bottomLeft2,
    // bottomRight
    fjdialog,
  },
  mounted() {
    this.cancelLoading();
    this.getCurrentDateTime();
    setInterval(() => {
      this.getCurrentDateTime();
    }, 1000);
  },
  methods: {
    cancelLoading() {
      setTimeout(() => {
        this.loading = false;
      }, 500);
    },
    getCurrentDateTime() {
      const date = new Date();
      const year = date.getFullYear();
      const month = this.addZero(date.getMonth() + 1);
      const day = this.addZero(date.getDate());
      const week = this.getWeekday(date.getDay());
      const hours = this.addZero(date.getHours());
      const minutes = this.addZero(date.getMinutes());
      this.currentDateTime = `${year}年${month}月${day}日 ${week} ${hours}:${minutes}`;
    },
    addZero(num) {
      return num < 10 ? `0${num}` : num;
    },
    getWeekday(day) {
      const weekdays = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"];
      return weekdays[day];
    },
    handleTabChange(tab) {
      this.currentTab = tab;
    },
  }
};
</script>

<style lang="scss">
@import "../assets/scss/index.scss";

.active {
  background-color: #1E90FF;
}

.LeftBottom {
  display: grid;
  grid-template-rows: 3.5fr 2fr;

}
</style>
