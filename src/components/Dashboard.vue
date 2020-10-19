<template>
  <b-container fluid>
    <b-row class="justify-content-md-center">
      <b-col cols md="6" sm="10" class="package-container">
        <package-creator style="margin-top: 5vh;"></package-creator>
      </b-col>
      <b-col cols md="4" sm="10" class="image-container">
        <image-preview
          align-v="center"
          class="text-center"
          style="margin-top: 15vh;"
        ></image-preview>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import PackageCreator from "./PackageCreator";
import ImagePreview from "./ImagePreview.vue";

export default {
  name: "Dashboard",
  components: {
    PackageCreator,
    ImagePreview,
  },
};
</script>

<style scoped>
.package-container {
  background-color: #cfcfcf;
  margin-top: 10vh;
  margin-inline-end: 2vw;
  border-radius: 25px 0;
  box-shadow: 0 0 0 3pt #0093c4;
}
.image-container {
  background-color: #cfcfcf;
  margin-inline-start: 1vw;
  margin-top: 10vh;
  border-radius: 0 25px;
  box-shadow: 0 0 0 3pt #0093c4;
}
</style>
