<template>
  <v-content>
    <v-toolbar></v-toolbar>
    <div class="detail-container">
      <h1 class="display-2">{{ product.name }}</h1>
      <div class="image-container">
        <img :src="product.imageUrl" alt="商品画像" class="mainImage">
      </div>
      <div class="price-container">
        <p class="headline" style="width:30%;">{{ product.price }}円</p>
        <p class="headline" style="width:70%;">
          数量：
          <Counter
            @on-minus="countMinus"
            @on-plus="countPlus"
          >{{ count }}</Counter>
        </p>
      </div>
      <CartButton
        @on-clicked="addToCart"
      > </CartButton>
      <p>{{ product.description }}</p>
      <p>出品URL：{{ product.url }}</p>
    </div>
  </v-content>
</template>

<script>
  const moment = require('moment')
  import axios from 'axios'
  import CartButton from '../components/CartButton'
  import Counter from '../components/Counter'

  export default {
    name: 'ProductDetail',
    components: {
      CartButton,
      Counter,
    },
    props: {
      janCode: String,
    },
    data () {
      return {
        product: {},
        appId: 'dj00aiZpPUQ4RTBUUTVSNUs3TyZzPWNvbnN1bWVyc2VjcmV0Jng9NTI-',
        apiUrl: 'https://shopping.yahooapis.jp/ShoppingWebService/V1/json/itemSearch',
        count: 1,
      }
    },
    computed: {
      totalPrice () {
        return Number(this.product.price) * this.count
      }
    },
    methods: {
      searchProduct () {
        axios.get(this.apiUrl, {
          params: {
            appid: this.appId,
            jan: this.janCode,
          }
        })
        .then((res) => {
          console.log(res)
          const resultData = res.data.ResultSet[0].Result[0]
          this.product = {
            name: resultData.Name,
            description: resultData.Description,
            url: resultData.Url,
            imageUrl: resultData.Image.Medium,
            thumbnailUrl: resultData.Image.Small,
            price: resultData.Price._value,
            janCode: resultData.JanCode,
          }
        })
      },
      countMinus () {
        this.count--
      },
      countPlus () {
        this.count++
      },
      addToCart () {
        firebase.database().ref('/cart_list/').push({
          name: this.product.name,
          price: this.product.price,
          thumbnailUrl: this.product.thumbnailUrl,
          janCode: this.product.janCode,
          count: this.count,
          addedAt: moment().format('YYYY/MM/DD HH:mm'),
        })
      },
    },
    mounted () {
      this.searchProduct()
    }
  }
</script>

<style scoped>
  .detail-container {
    margin: 5vw;
  }
  .image-container {
    text-align: center;
  }
  .mainImage {
    width: 80vw;
  }
  .price-container {
    display: flex;
    text-align:center;
  }
  .price-content {
    width: 50%;
  }
  .cart-icon {
    font-size: 7vw;
    margin-right: 3vw;
  }
</style>
