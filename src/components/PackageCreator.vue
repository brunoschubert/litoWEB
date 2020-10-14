<template>
  <b-form @submit="onSubmit" @reset="onReset" v-if="show">
    <b-form-input
      class="input-field"
      v-model="form.name"
      required
      placeholder="Enter sample name"
    ></b-form-input>
    <div class="mt-3">Name: {{ form.name }}</div>

    <b-form-textarea
      class="input-field"
      v-model="form.description"
      placeholder="Enter sample description"
      size="md"
    ></b-form-textarea>
    <div class="mt-3">Selected file: {{ form.description }}</div>

    <b-row class="justify-content-md-center">
      <b-col cols md="6" sm="10">
        <b-form-file
          class="input-field"
          v-model="form.modelFile"
          placeholder="Choose your sample's model or drop it here."
        ></b-form-file>
      </b-col>

      <b-col cols md="6" sm="10">
        <b-form-file
          class="input-field"
          v-model="form.modelTexture"
          placeholder="Choose your sample's texture or drop it here."
        ></b-form-file>
      </b-col>
    </b-row>
    <div class="mt-3">Selected model: {{ form.modelFile }}</div>
    <div class="mt-3">Selected texture: {{ form.modelTexture }}</div>

    <b-form-file
      class="input-field"
      v-model="form.images"
      multiple
      placeholder="Choose your sample's images or drop them here."
    ></b-form-file>
    <div class="mt-3">Selected file: {{ file2 ? file2.name : "" }}</div>

    <b-form-file
      class="input-field"
      v-model="form.documents"
      multiple
      directory
      placeholder="Choose your sample's documents or drop them here."
    ></b-form-file>
    <div class="mt-3">Selected file: {{ file2 ? file2.name : "" }}</div>

    <b-button type="submit" variant="primary">Submit</b-button>
    <b-button type="reset" variant="danger">Reset</b-button>
  </b-form>
</template>

<script>
export default {
  name: "PackageCreator",
  data() {
    return {
      form: {
        name: "",
        description: "",
        modelFile: null,
        modelTexture: null,
        images: [],
        documents: [],
      },
      show: true,
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      console.log(JSON.stringify(this.form));
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.name = "";
      this.form.description = "";
      this.form.modelFile = null;
      this.form.modelTexture = null;
      this.form.images = [];
      this.form.documents = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>

<style scoped>
.input-field {
  margin-top: 2.5vh;
  margin-bottom: 2.5vh;
}
</style>
