<template>
    <div class="item--quantity">
        <button class="buttons" @click="decreaseQuantity(item.id)" :disabled="item.quantity == 0">-</button>
        <span class="number"> {{ item.quantity }}</span>
        <button class="buttons" @click="increaseQuantity(item.id)">+</button>
    </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
    props: {
        item: {}
    },
    methods: {
        ...mapActions([
            'increaseQuantity',
            'decreaseQuantity'
        ])
    }
};
</script>

<style lang="less" scoped>
.item--quantity {
    display: flex;
    align-items: center;

    .number {
        font-weight: 500;
        font-size: 18px;
        color: @blue;
        width: 28px;
        text-align: center;
    }

    .buttons {
        font-weight: 600;
        font-size: 18px;
        cursor: pointer;
        background: none;
        border: 0;
        color: @write;


        &focus {
            outline: 0;
        }
    }
}
</style>