<template>
  <b-form @submit="onSubmit" @reset="onReset" v-if="show">
    <b-form-input
      class="input-field"
      v-model="name"
      required
      placeholder="Enter sample name"
    ></b-form-input>

    <b-form-textarea
      class="input-field"
      v-model="description"
      required
      placeholder="Enter sample description"
      size="md"
    ></b-form-textarea>

    <b-row class="justify-content-md-center">
      <b-col cols md="6" sm="10">
        <b-form-file
          class="input-field"
          v-model="modelFile"
          required
          placeholder="Choose your sample's model or drop it here."
        ></b-form-file>
      </b-col>

      <b-col cols md="6" sm="10">
        <b-form-file
          class="input-field"
          v-model="modelTexture"
          required
          placeholder="Choose your sample's texture or drop it here."
        ></b-form-file>
      </b-col>
    </b-row>

    <b-form-file
      class="input-field"
      v-model="modelMaterial"
      required
      placeholder="Choose your sample's material or drop it here."
    ></b-form-file>

    <b-form-file
      class="input-field"
      v-model="images"
      required
      multiple
      placeholder="Choose your sample's images or drop them here."
    ></b-form-file>

    <b-form-file
      class="input-field"
      v-model="documents"
      multiple
      directory
      placeholder="Choose your sample's documents or drop them here."
    ></b-form-file>

    <b-button type="submit" variant="primary">Submit</b-button>
    <b-button type="reset" variant="danger">Reset</b-button>
  </b-form>
</template>

<script>
import JsZip from "jszip";
import FileSaver from "file-saver";

export default {
  name: "PackageCreator",
  data() {
    return {
      name: "",
      description: "",
      sampleTAG: {},
      modelFile: null,
      modelMaterial: null,
      modelTexture: null,
      images: [],
      documents: [],
      show: true,
    };
  },
  watch: {
    name() {
      let data = this.name + this.description;
      this.$root.$emit("upadateTAG", data);
    },
    description() {
      let data = this.name + this.description;
      this.$root.$emit("upadateTAG", data);
    },
  },
  mounted() {
    this.$root.$on("newTAGImage", (data) => {
      this.sampleTAG = data;
    });
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.generatePackage();
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.name = "";
      this.description = "";
      this.arTAG = null;
      this.modelFile = null;
      this.modelMaterial = null;
      this.modelTexture = null;
      this.images = [];
      this.documents = [];

      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    generatePackage() {
      // Define File Paths.
      let modelpath = "model/";
      let imgPath = "images/";
      let docPath = "documents/";

      // Create JSON Package.
      let packageJSON = this.createJSON(modelpath, imgPath, docPath);
      let packageName = "package.json";

      // console.log("===================");
      // console.log(JSON.stringify(packageJSON));
      // console.log("===================");

      // Create the Zip Object{} that hold files.
      let zip = new JsZip();

      // Create Folder Structure.
      zip.file(packageName, JSON.stringify(packageJSON));

      // Makes sure it encodes just the Data. Not the DataURL
      zip.file(this.name + "TAG.png", this.sampleTAG.sampleTag, {
        base64: true,
      });
      //zip.file(this.name + "TAG.png", this.sampleTAG, { binary: true });

      zip.file(modelpath + this.modelFile.name, this.modelFile);

      zip.file(modelpath + this.modelMaterial.name, this.modelTexture);

      zip.file(modelpath + this.modelTexture.name, this.modelTexture);

      for (let i = 0; i < this.images.length; i++) {
        let image = this.images[i];
        zip.file(imgPath + image.name, image);
      }

      for (let i = 0; i < this.documents.length; i++) {
        let doc = this.doc[i];
        zip.file(docPath + doc.name, doc);
      }

      // Save the AR Tag.
      FileSaver.saveAs(this.sampleTAG.dataUrl, this.name + "TAG.png");

      // Create the Package File and Download it.
      zip.generateAsync({ type: "blob" }).then(function(content) {
        FileSaver.saveAs(content, "package.zip");
      });
    },
    createJSON(modelpath, imgPath, docPath) {
      let packageJSON = {};
      packageJSON.name = this.name;
      packageJSON.description = this.description;
      packageJSON.sampleTAG = this.name + "TAG.png";

      packageJSON.model = {};
      packageJSON.model.modelFile = "/" + modelpath + this.modelFile.name;
      packageJSON.model.modelMaterial =
        "/" + modelpath + this.modelMaterial.name;
      packageJSON.model.modelTexture = "/" + modelpath + this.modelTexture.name;

      packageJSON.imgPath = "/" + imgPath;
      packageJSON.docPath = "/" + docPath;

      return packageJSON;
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
