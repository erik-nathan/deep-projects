<template>
  <div class="payment">
      <div class="payment--content">
            <router-link to="/" class="payment--go-back">⬅ Voltar</router-link>
      </div>      
      <Cart v-if="isDesktop()" />
  </div>
</template>

<script>
import Mixin from '@/mixins/mixins'
import Cart from '../components/cart.vue'
export default {
  components: {
    Cart
  },
   mixins: [Mixin]
}
</script>

<style lang="less" scoped>
 .payment {
   display: flex;

   &--content {
     flex-grow: 1;
     padding: 50px;
   
    .payment--go-back {
    font-weight: 600;
    font-size: 18px;
    text-decoration: none;
    color: @write;
    }
  }
 }

</style>