<template>
  <v-content>
    <v-toolbar></v-toolbar>
      <Scanner
        @scan-completed="searchProduct"
      ></Scanner>
      <TopMenuButton
        icon="fa-history"
        label="注文履歴"
        @on-clicked=""
      ></TopMenuButton>
  </v-content>
</template>
<script>
  import axios from 'axios'
  import Scanner from '../components/Scanner'
  import TopMenuButton from '../components/TopMenuButton'

  export default{
    name: 'TopMenu',
    components: {
      Scanner,
      TopMenuButton,
    },
    data () {
      return {
        title: 'My app',
        appId: 'dj00aiZpPUQ4RTBUUTVSNUs3TyZzPWNvbnN1bWVyc2VjcmV0Jng9NTI-',
        apiUrl: 'https://shopping.yahooapis.jp/ShoppingWebService/V1/json/itemSearch',
      }
    },
    methods: {
      searchProduct (jan) {
        axios.get(this.apiUrl, {
          params: {
            appid: this.appId,
            jan: jan,
          }
        })
        .then((res) => {
          const resultData = res.data.ResultSet[0].Result[0]
          if (resultData) {
            this.$router.push({
              name: 'product_detail',
              params: {
                product: {
                  name: resultData.Name,
                  description: resultData.Description,
                  url: resultData.Url,
                  imageUrl: resultData.Image.Medium,
                  thumbnailUrl: resultData.Image.Small,
                  price: resultData.Price._value,
                  janCode: resultData.JanCode,
                }
              }
            })
          }
        })
      }
    }
  }
</script>
