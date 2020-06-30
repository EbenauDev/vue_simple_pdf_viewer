<template>
  <div>
    <label class="button" v-searchPDF="{callback: resultSearchPDF}">
      <input type="file" hidden accept="application/pdf" />
      Search PDF
    </label>
    <div v-if="arrayDeBits" style="margin-top:20px">
      <h3>Number of pages: {{numberPages}}</h3>
      <div>
        <button class="button" @click="currentPage -= 1" :disabled="currentPage == 1">Prev page</button>
        <button
          class="button"
          @click="currentPage +=  1"
          :disabled="currentPage == numberPages"
        >Next page</button>
      </div>
      <pdf
        @num-pages="numberPages = $event"
        :page="currentPage"
        :src="arrayDeBits"
        style="display: inline-block;width: 80vw;"
      ></pdf>
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
  data() {
    return {
      arrayDeBits: null,
      numberPages: 1,
      currentPage: 1
    };
  },
  methods: {
    resultSearchPDF(response) {
      this.arrayDeBits = new Uint8Array(response);
    },
    documentHasBeenLoaded() {
      console.log("Documento foi carregado!");
    },
    numberOfPages() {
      console.log("Number of pages!");
    }
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
  margin: 10px 20px;
  &:active {
    filter: contrast(0.8);
  }
}
h3 {
  color: #ffffff;
}
</style>