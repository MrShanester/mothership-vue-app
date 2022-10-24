<template>
  <div id="app">
    <button v-on:click="generatePDF()">Generate PDF</button>
    <!-- <div @click="generatePDF()" class="np-btn">Generate PDF</div> -->

    <vue-html2pdf
      :show-layout="false"
      :float-layout="true"
      :enable-download="false"
      :preview-modal="true"
      :paginate-elements-by-height="1920"
      filename="Mothership Character Sheet"
      :pdf-quality="2"
      :manual-pagination="true"
      pdf-format="a4"
      :pdf-margin="10"
      pdf-orientation="landscape"
      pdf-content-width="1080px"
      @progress="onProgress($event)"
      ref="html2Pdf"
    >
      <section slot="pdf-content">
        <ContentToPrint />
      </section>
    </vue-html2pdf>
    <div id="center">
      <ContentToPrint />
    </div>
  </div>
</template>

<script>
import VueHtml2pdf from "vue-html2pdf";
import ContentToPrint from "./ContentToPrint";

export default {
  name: "App",
  methods: {
    onProgress(event) {
      console.log(`Processed: ${event} / 100`);
    },
    hasGenerated() {
      alert("PDF generated successfully!");
    },
    generatePDF() {
      this.$refs.html2Pdf.generatePdf();
    },
  },
  components: {
    VueHtml2pdf,
    ContentToPrint,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.np-btn {
  padding: 2px 8px;
  margin: 12px 8px;
  border: 1px solid #da1010;
  width: 110px;
  background: #da1010;
  border-radius: 6px;
  color: #ffffff;
  cursor: pointer;
}

#center {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
