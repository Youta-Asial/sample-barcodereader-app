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
          <v-btn icon @click="countMinus">
            <v-icon class="counter">fa-minus-circle</v-icon>
          </v-btn>
          <span>{{ count }}</span>
          <v-btn icon @click="countPlus">
            <v-icon class="counter">fa-plus-circle</v-icon>
          </v-btn>
        </p>
      </div>
      <v-btn block large class="cart-btn">
        <v-icon class="cart-icon">fa-shopping-cart</v-icon>
        カートに入れる
      </v-btn>
      <p>{{ product.description }}</p>
      <p>出品URL：{{ product.url }}</p>
    </div>
  </v-content>
</template>

<script>
  export default {
    name: 'ProductDetail',
    props: {
      product: {
        type: Object,
        default: () => {
          return {
            name: 'Dr Pepper',
            description: 'ドドクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパードクターペッパークターペッパー',
            url: 'dokupe.yahoo.jp',
            imageUrl: 'hogw',
            thumbnailUrl: 'hogeho',
            price: 100,
          }
        }
      }
    },
    data () {
      return {
        count: 1,
        maxCount: 99,
      }
    },
    computed: {
      totalPrice () {
        return Number(this.product.price) * this.count
      }
    },
    methods: {
      countPlus () {
        if (this.count <= this.maxCount) {
          this.count++
        }
      },
      countMinus () {
        if (this.count > 1) {
          this.count--
        }
      },
    },
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
  .counter {
    padding-bottom: 2px;
  }
  .cart-btn {
    font-size: 4vw;
  }
  .cart-icon {
    font-size: 7vw;
    margin-right: 3vw;
  }
</style>
