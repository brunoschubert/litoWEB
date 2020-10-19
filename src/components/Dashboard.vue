<template>
  <b-container fluid>
    <b-row class="justify-content-md-center">
      <b-col cols md="6" sm="10" class="package-container">
        <package-creator style="margin-top: 5vh;"></package-creator>
      </b-col>
      <b-col cols md="4" sm="10" class="image-container">
        <image-preview></image-preview>
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
  background-color: #e0e0e0;
  margin-top: 5vh;
  margin-inline-end: 2vw;
  border-radius: 25px 0;
  box-shadow: 0 0 0 3pt #0093c4;
}
.image-container {
  background-color: #e0e0e0;
  margin-inline-start: 1vw;
  margin-top: 5vh;
  border-radius: 0 25px;
  box-shadow: 0 0 0 3pt #0093c4;
}
</style>
