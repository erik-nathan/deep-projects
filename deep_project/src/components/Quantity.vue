<template>
    <div class="item--quantity">
        <button class="buttons" @click="onDecreaseButtonClick" :disabled="item.quantity == 0">-</button>
        <span class="number"> {{ item.quantity }}</span>
        <button class="buttons" @click="onIncreaseButtonClick">+</button>
    </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
    props: {
        item: {},
        useStore: {
            type: Boolean,
            default: true
        }
    },
    methods: {
        ...mapActions([
            'increaseQuantity',
            'decreaseQuantity'
        ]),
        onDecreaseButtonClick() {
            if(this.useStore) {
                this.decreaseQuantity(this.item.id);
                return;
            }
            --this.item.quantity;
        },
        onIncreaseButtonClick(){
           if(this.useStore) {
                this.increaseQuantity(this.item.id);
                return;
            }
            ++this.item.quantity;
        }

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