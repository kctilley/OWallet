<style scoped>
.changelly-container {
  position: relative;
  padding-bottom: 75%;
  height: 0;
  overflow: hidden;
}
.changelly-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
<template>
    <div>
      <breadcrumb  :current="$t('exchange.exchange')" v-on:backEvent="handleRouteBack"></breadcrumb>
      <!-- Remove this div and enable this.loadPage in mounted() to open in a new window -->
      <div class="changelly"
        <iframe src="https://widget.changelly.com?currencies=&from=btc&to=ont&amount=1&address=&fiat=true&fixedTo=false&theme=default&ref_id=su5srryl1mhz4fno&merchant_id=su5srryl1mhz4fno" width="100%" height="600" class="changelly" scrolling="no" onLoad="function v(e){var t=e.target,n=t.parentNode,r=t.contentWindow,a=function(){return r.postMessage({width:n.offsetWidth},'https://widget.changelly.com')};window.addEventListener('resize',a),a()};v.apply(this, arguments);" style="overflow-y: hidden; border: none">Can't load widget</iframe>
      </div>
</template>

<script>
import Breadcrumb from "../../Breadcrumb";
const changellyURL =
  "https://changelly.com/widget/v1?from=BTC&to=ONT&merchant_id=pzjsilenplyn7jgd&address=&amount=1&ref_id=pzjsilenplyn7jgd&color=196BD8";
const { BrowserWindow } = require("electron").remote;

export default {
  name: "Changelly",
  mounted() {
    //Changelly page set to load as iframe in current window, if new browser
    //window is preferred, enable method this.loadPage() below and remove reference
    //to iFrame in <div> above
    //this.loadPage()
  },
  data() {
    return {};
  },
  components: {
    Breadcrumb
  },
  methods: {
    handleRouteBack() {
      this.$router.push({ name: "Exchange" });
    },
    loadPage() {
      let win = new BrowserWindow({ width: 1000, height: 550, center: true });
      win.on("closed", () => {
        win = null;
      });
      win.loadURL(changellyURL);
    }
  }
};
</script>