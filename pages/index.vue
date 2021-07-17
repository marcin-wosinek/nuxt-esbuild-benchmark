<template>
  <div>
    <button v-on:click="generatePdf">Generate pdf</button>

    <br />

    <iframe style="width: 350px; height: 600px" v-bind:src="pdf"></iframe>
  </div>
</template>

<script>
const { PDFDocument } = require("pdf-lib");

export default {
  data() {
    return {
      pdf: "",
    };
  },

  methods: {
    async generatePdf() {
      const pdfDoc = await PDFDocument.create();
      const page = pdfDoc.addPage([350, 400]);
      page.moveTo(110, 200);
      page.drawText("Hello World!");
      const pdfDataUri = await pdfDoc.saveAsBase64({ dataUri: true });
      this.pdf = pdfDataUri;
    }
  }
};
</script>
