<template>
  <div>
    <label class="button" v-searchPDF="{callback: resultSearchPDF}">
      <input type="file" hidden accept="application/pdf" />
      Search PDF
    </label>
    <div v-if="arrayDeBits">
      <pdf :src="arrayDeBits"></pdf>
    </div>
  </div>
</template>

<script>
import pdf from "vue-pdf";
export default {
  name: "PDFViewer",
  components: {
    pdf
  },
  directives: {
    searchPDF: function(el, binding) {
      const input = el.querySelector("input");

      const fileReader = new FileReader();
      input.addEventListener("change", handleFile, false);

      function handleFile({ target }) {
        fileReader.readAsArrayBuffer(target.files[0]);
        fileReader.onload = () => {
          getResultReadFile(fileReader.result);
        };
      }
      function getResultReadFile(file) {
        binding.value.callback && binding.value.callback(file);
      }
    }
  },
  methods: {
    resultSearchPDF(response) {
      this.arrayDeBits = new Uint8Array(response);
    }
  },
  data() {
    return {
      arrayDeBits: null
    };
  }
};
</script>

<style lang="scss" scoped>
.button {
  padding: 10px 20px;
  cursor: pointer;
  border: 0;
  border-radius: 4px;
  background-color: #ffffff;
  &:active {
    filter: contrast(0.8);
  }
}
</style>