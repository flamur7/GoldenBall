<template>
  <VueDropzone
    id="dropzone"
    ref="filesDropzone"
    :options="dropzoneOptions"
    :useCustomSlot="true"
    @vdropzone-mounted="handleMount"
    @vdropzone-removed-file="removeFile"
    :destroyDropzone="false"
    class="rounded-lg mb-4"
  >
    <div class="justify-content-center">
      <h3 class="text-success font-weight-bold">
        Drag and drop to upload files
      </h3>
      <div>...or click to select from ur pc</div>
    </div>
  </VueDropzone>
</template>

<script>
import VueDropzone from "vue2-dropzone";
import "vue2-dropzone/dist/vue2Dropzone.min.css";
import apiRequest from "../../utility/apiRequest";

export default {
  components: {
    VueDropzone,
  },
  props: {
    playerId: String,
    initialFiles: String,
  },
  data() {
    return {
      dropzoneOptions: {
        url: `http://localhost:4000/player/${this.playerId}/uploadFile`,
        method: "put",
        thumbnailWidth: 300,
        maxFilesize: 2,
        addRemoveLinks: true,
      },
    };
  },
  methods: {
    removeFile(file) {
      apiRequest.removeFile(this.vueshopId, file);
    },

    async handleMount() {
      if (!this.initialFiles || this.initialFiles.length === 0) {
        return;
      }

      const documentFiles = await apiRequest.getFilesDetails(this.initialFiles);

      documentFiles.forEach(({ fileDetails, fileUrl }) => {
        this.$refs.filesDropzone.manuallyAddFile(
          fileDetails,
          `http://localhost:4000/${fileUrl}`
        );
      });
    },
  },
};
</script>
