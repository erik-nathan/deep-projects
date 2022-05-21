<template>
  <div class="home">
    <CartIcon />
    <CategoryMenu />
    <ItemsList /> 
    <Cart v-if="isDesktop()" />
  </div>
</template>

<script>
import CategoryMenu from '@/components/CategoryMenu.vue'
import ItemsList from '@/components/ItemsList.vue'
import Cart from '../components/cart.vue'
import Mixin from '@/mixins/mixins'
import CartIcon from '@/assets/icons/cart.svg'



export default {
  name: 'HomeView',
  components: {
    CategoryMenu,
    ItemsList,
    Cart, 
    CartIcon
  },
  mixins: [Mixin]
}
</script>

<style scoped lang="less">
  .home{
    display: flex;

    @media @tablets {
      flex-direction: column;
    }
  }
</style>