<template>
  <div class="pdf-container"></div>
</template>

<script>
import PSPDFKit from "pspdfkit";

export default {
  name: "PSPDFKit",
  /**
   * The component receives `pdfFile` prop which is type of String and required
   */
  props: {
    pdfFile: {
      type: String,
      required: true,
    },
  },
  /**
   * We wait until the template has been rendered to load the document into the library.
   */
  mounted() {
    this.loadPSPDFKit().then((instance) => {
      this.$emit("loaded", instance);
    });
  },
  /**
   * We watch for `pdfFile` prop changes and trigger unloading and loading when there's a new document to load.
   */
  watch: {
    pdfFile(val) {
      if (val) {
        this.loadPSPDFKit();
      }
    },
  },
  /**
   * Our component has `loadPSPDFKit` method, this unloads and cleanup the component and triggers document loading.
   */
  methods: {
    async loadPSPDFKit() {
      PSPDFKit.unload(".pdf-container");
      return PSPDFKit.load({
        // access the pdfFile from props
        locale: "ja",
        document: this.pdfFile,
        container: ".pdf-container",
        licenseKey:
          "zY7aX0blzVGyQasPRUMP2oVyGFo2Tfsnmb_iW4_5Lg4eE1vw4s2WeJaajnubgL8tYhpdIJKycml_-27aIpj7llTnVOJ4krE_y7Uc4RAwQtCSR-YAU9V0wxqJYe2f5mdf4MUhSXTJ8PZorOgvXkWbTdBRl68sV4e40MIWJujpg9yA_DPAr5EWcEzcWewNwdA1gXRhxe8P55n7dJCcr59l9LEdbIjOCNtVyfPgfuOKEcFCmtTK4HbOL9Zb0eVrQP19dI2rUWqrFGPMCVHycv6XIz70ujSK2Ce-rJ6HvPERpTCN9l9dP3WPDszB0ZVYxgc-UxGO5DZHEowTf8EQpWKX63j6sgoIaRit1He0Ml0DqqSOIeXIK2bPFT2TQ0GeEyestspotBA1t5UucFNS1XlUQNwYU8Ch5trzvKpk62ii_R4fMFPhYhSwE_oJXODkVTvB0fKdh9yTV_YybseAcDqCWQ-_R5GAP3DGxXHSb2lrpdvglRA1yGiSOqBjfoVeu42Yk_njfWwh6S8D8ScN-6zeQTl0CZvgQyDYR3D46punwhUj119FSvrJc6FE9Y-9W0sRIKOX7IgBn718CB2eg7EHmA==",
      });
    },
  },

  /**
   * Clean up when the component is unmounted; so, it is ready to load another document.
   */
  beforeUnmount() {
    PSPDFKit.unload(".pdf-container");
  },
};
</script>

<style scoped>
.pdf-container {
  height: 100vh;
}
</style>
