<template>
  <TopMenuButton
    icon="fa-barcode"
    label="バーコードスキャン"
    @on-clicked="scanBarcode"
  ></TopMenuButton>
</template>

<script>
  import TopMenuButton from './TopMenuButton'

  export default{
    name: 'Scanner',
    components: {
      TopMenuButton
    },
    data() {
      return {
        product: {},
      }
    },
    methods: {
      scanBarcode () {
        window.plugins.barcodeScanner.scan(
          this.scanSuccess,
          function(error) {
            alert("Scanning failed: " + error);
          })
      },
      scanSuccess (result) {
        console.log('scan success!')
        this.$emit('scan-completed', result.text)
      },
    }
  }
</script>
