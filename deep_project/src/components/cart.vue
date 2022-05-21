<template>
  <div class="cart">
      <router-link to="/" class="cart--go-back">- Voltar</router-link>
      <h2 class="cart--title"> Seu Pedido </h2>
      <CartItem v-for="item in cartList" :key="item.id" :item="item"/>
      <div class="cart--total">
          <span>Total: </span>
          <span class="price">{{getCartTotal | currency}}</span>
      </div>
  </div>
</template>

<script>
import CartItem from './cartItem';
import { mapGetters } from 'vuex';

export default {
 name: 'Cart',
 components: {
     CartItem
 },
 filters: {
        currency(value){
            return `R$ ${value.toLocaleString('pt-br', { minimumFractionDigits : 2})}`
        }
    },
 computed: {
     ...mapGetters([
         'getCartTotal'
     ]),
     cartList(){
         return this.$store.state.cartList;
     }
 }
}
</script>

<style lang="less" scoped>
    .cart{
        background: @light-grey;
        width: 643px;
        min-width: 643px;
        padding: 50px;

         &--title {
             font-weight: 600;
             font-size: 24px;
             margin-top: 50px;
             color: @write;
         }

        &--total {
            font-weight: 600;
            font-size: 18px;
            text-align: right;
            margin-top: 30px;
            
            .price{
               color: @blue; 
               padding-left: 10px;
            }
         }

          &--go-back {
             font-weight: 600;
             font-size: 18px;
             text-decoration: none;
             color: @write;
         }

         @media @tablets {
            //  background: @bg-color;
             width: 100%;
             min-width: unset;
             padding: 50px 20px 20px;
         }
    }

   

</style>