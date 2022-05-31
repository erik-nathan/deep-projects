<template>
    <div class="cart">
        <router-link to="/" class="cart--go-back" v-if="isSmallScreen()">⬅ Voltar</router-link>
        <h2 class="cart--title"> Seu Pedido </h2>
        <div class="cart--content">
            <p v-if="!hasItems" class="cart--p">Seu carrinho ainda está vazio.</p>
        <transition-group name="list">
            <CartItem v-for="item in cartList" :key="item.id" :item="item" />
        </transition-group>
    </div>
        <div class="cart--total" v-if="hasItems">
            <span>Total: </span>
            <span class="price">{{ getCartTotal | currency }}</span>
        </div>
        <button class="primary-button payment-button" v-if="!!cartList.length" @click="goToPayment">Finalizar compra</button>
    </div>
</template>

<script>
import CartItem from './cartItem';
import { mapGetters } from 'vuex';
import Mixin from '@/mixins/mixins';

export default {
    name: 'Cart',
    mixins: [Mixin],
    components: {
    CartItem
    },
    filters: {
        currency(value) {
            return `R$ ${value.toLocaleString('pt-br', { minimumFractionDigits: 2 })}`
        }
    },
    computed: {
        ...mapGetters([
            'getCartTotal'
        ]),
        cartList() {
            return this.$store.state.cartList;
        },
        hasItems() {
            return this.cartList.length;
        }
    },
     methods: {
        goToPayment() {
            this.$router.push({ name: 'Payment' });
        }
    }
};
</script>

<style lang="less" scoped>
.cart {
    background: @light-grey;
    width: 643px;
    height: 100vh;
    min-width: 643px;
    padding: 50px;
    display: flex;
    flex-direction: column;

    &--go-back {
        font-weight: 600;
        font-size: 18px;
        text-decoration: none;
        color: @write;
    }

    &--title {
        font-weight: 600;
        font-size: 24px;
        margin-top: 50px;
        color: @write;
    }

    &--content {
        flex-grow: 1;
        overflow: auto;
    }

    &--p {
        color: @colorDesc;
    }

    &--total {
        font-weight: 600;
        font-size: 18px;
        text-align: right;
        margin-top: 30px;
        color: @write;

        .price {
            color: @blue;
            padding-left: 10px;
        }
    }

    .payment-button {
        width: 397px;
        margin: 20px auto;
    }

    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }
    .list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
        opacity: 0;
        transform: translateY(30px);
    }

    @media @tablets {
        //  background: @bg-color;
        width: 100%;
        min-width: unset;
        padding: 50px 20px 20px;

        .payment-button {
            width: 100%;
        }
    }
}
</style>