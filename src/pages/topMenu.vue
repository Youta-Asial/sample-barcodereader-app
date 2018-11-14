<template>
  <v-content>
    <Header>
      <template slot="title">商品検索アプリ</template>
    </Header>
      <Scanner
        @scan-completed="goToProductDetail"
      ></Scanner>
      <TopMenuButton
        icon="fa-shopping-cart"
        label="カート一覧"
        @on-clicked="goToCartList"
      ></TopMenuButton>
      <!-- TODO: 注文機能・注文履歴機能は未実装 -->
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
  import Header from '../components/Header'

  export default{
    name: 'TopMenu',
    components: {
      Scanner,
      TopMenuButton,
      Header,
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
