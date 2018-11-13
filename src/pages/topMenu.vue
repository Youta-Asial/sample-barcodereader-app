<template>
  <v-content>
    <v-toolbar></v-toolbar>
      <Scanner
        @scan-completed="goToProductDetail"
      ></Scanner>
      <TopMenuButton
        icon="fa-shopping-cart"
        label="カート"
        @on-clicked="goToCartList"
      ></TopMenuButton>
      <TopMenuButton
        icon="fa-history"
        label="注文履歴"
        @on-clicked=""
      ></TopMenuButton>
  </v-content>
</template>
<script>
  import Scanner from '../components/Scanner'
  import TopMenuButton from '../components/TopMenuButton'

  export default{
    name: 'TopMenu',
    components: {
      Scanner,
      TopMenuButton,
    },
    methods: {
      goToProductDetail (janCode) {
        this.$router.push({
          name: 'product_detail',
          params: { janCode: janCode, },
        })
      },
      goToCartList () {
        this.$router.push({
          name: 'cart_list',
        })
      }
    }
  }
</script>
