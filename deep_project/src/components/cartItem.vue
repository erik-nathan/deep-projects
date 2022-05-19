<template>
  <div class="item">
      <div class="item--img-container">
        <img class="item--img" :src="imagePath" >
      </div>
     
      <div class="content">
          <h3 class="item--name">{{item.name}}</h3>
          <a class="item--observation"> Adicionar Observação</a>
      </div>
      <p class="item--price">{{item.price | currency}} </p>
  </div>
</template>

<script>
export default {
    name: 'CartItem',
    props: {
        item: {}
    },
     filters: {
        currency(value){
            return `R$ ${value.toLocaleString('pt-br', {minimumFractionDigits:2})}`
        }
    },
    computed: {
        selectedCategory() {
            return this.$store.state.selectedCategory;
        },
        imagePath() {
            return require(`../assets/images/${this.selectedCategory}/${this.item.id}.png`)
        }
    }
}
</script>

<style lang="less" scoped>
    .item{
        display: flex;
        border-bottom: 1px solid @colorDesc;
        padding: 20px 0;

        &--img-container{
           border-radius: 8px;
           background: @bg-color;
           width: 81px;
           height: 66px;
           display: flex;
           align-items: center;
        }

        &--img{
            width: 65px;
            display: block;
            margin: auto;

        }

        &--name{
          font-weight: 600;
          font-size: 18px;
          margin: 0;
          color: @write
        }

         &--observation{
          font-weight: 500;
          font-size: 12px;
          color: @colorDesc;
          text-decoration: underline;
        }

        .content{
            flex-grow: 1;
            padding: 0 20px;
        }

          &--price{
          font-weight: 600;
          font-size: 18px;
          margin: 0;
          color: @blue;
        }
    }
</style>