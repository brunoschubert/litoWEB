<template>
  <b-container fluid>
    <b-row class="justify-content-md-center">
      <b-col cols md="6" sm="10" style="background-color: #ff0000;">
        <package-creator style="margin-top: 5vh;"></package-creator>
      </b-col>
      <b-col cols md="4" sm="10" style="background-color: #00ff00;">
        <image-preview style="margin-top: 5vh;"></image-preview>
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

<style scoped></style>
