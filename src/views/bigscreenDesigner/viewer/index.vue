<!--
 * @Descripttion: 大屏设计器 -- 预览
 * @Author: lide1202@hotmail.com
 * @Date: 2021-3-13 11:04:24
 * @Last Modified by:   lide1202@hotmail.com
 * @Last Modified time: 2021-3-13 11:04:24
 !-->
<template>
  <div class="layout">
    <div :style="bigScreenStyle">
      <widget
        v-for="(widget, index) in widgets"
        :key="index"
        v-model="widget.value"
        :type="widget.type"
      />
    </div>
  </div>
</template>

<script>
import widget from "../designer/widget/temp";
// import { detailDashboard } from "@/api/bigscreen";
export default {
  name: "Viewer",
  components: {
    widget
  },
  data() {
    return {
      bigScreenStyle: {},
      widgets: []
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
       getImage(url) {
      return url.includes('http') ? url : require(`@/assets/images/items${url}.png`)
    },
    async getData() {
      // const reportCode = this.$route.query.reportCode;
      // const { code, data } = await detailDashboard(reportCode);
      // if (code != 200) return;
   
      const {dashboard} = JSON.parse(localStorage.getItem('viewParams'))
      const equipment = document.body.clientWidth;
      const ratioEquipment = equipment / dashboard.width;
      this.bigScreenStyle = {
        width: dashboard.width + "px",
        height: dashboard.height + "px",
        "background-color": dashboard.backgroundColor,
        "background-image": "url(" + this.getImage(dashboard.backgroundImage) + ")",
        "background-position": "0% 0%",
        "background-size": "100% 100%",
        "background-repeat": "initial",
        "background-attachment": "initial",
        "background-origin": "initial",
        "background-clip": "initial",
        transform: `scale(${ratioEquipment}, ${ratioEquipment})`,
        "transform-origin": "0 0"
      };
      this.widgets = dashboard.widgets;
    }
  }
};
</script>

<style scoped lang="scss">
.layout {
  width: 100%;
  height: 100%;
  text-align: center;
}
.bottom-text {
  width: 100%;
  color: #a0a0a0;
  position: fixed;
  bottom: 16px;
  z-index: 9999;
}
</style>
