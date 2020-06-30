<template>
  <div>
    <button v-searchPDF.funcoes="{callback: resultSearchPDF}">Search PDF</button>
  </div>
</template>

<script>
export default {
  name: "PDFViewer",
  directives: {
    searchPDF: function(el, binding) {
      console.log(el);
      console.log(binding);
      binding.value.callback("teste");
    }
  },
  methods: {
    resultSearchPDF(response) {
      console.log(response);
    }
  }
};
</script>

<style lang="scss" scoped>
button {
  padding: 10px 20px;
}
</style>