<template>
  <div>
    <h1 class="text-title">AR TAG</h1>
    <vue-qrcode
      id="tag"
      :value="code"
      :options="{ width: 300, margin: 0 }"
    ></vue-qrcode>
  </div>
</template>

<script>
import VueQrcode from "@chenfengyuan/vue-qrcode";
export default {
  name: "ImagePreview",
  components: { VueQrcode },
  data() {
    return {
      code: "default",
    };
  },
  watch: {
    code() {
      // Change to oncanvaschanged(e)?
      this.$nextTick(() => {
        let data = {};
        data.dataUrl = document.getElementById("tag").toDataURL("image/png");
        data.sampleTag = document
          .getElementById("tag")
          .toDataURL("image/png", [0.0, 1.0])
          .split(",")[1];
        this.$root.$emit("newTAGImage", data);
      });
    },
  },
  mounted() {
    this.$root.$on("upadateTAG", (data) => {
      this.code = data;
    });
  },
};
//document.getElementsByTagName("canvas")[0].toDataURL("image/png")
</script>

<style>
.text-title {
  margin-top: 5vh;
  color: rgb(66, 66, 66);
}
#tag {
  margin-top: 10vh;
}
</style>
