<template>
  <div class="category-menu">
    <ul>
      <li
        v-for="category in categoriesList"
        :key="category.id"
        @click="onCategoryClick(category.id)"
        :class="{ active: isActive(category.id) }"
      >
        <component :is="category.icon" />
        <p>{{ category.label }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import Iphones from "../assets/icons/smartphone.svg";
import Ipad from "../assets/icons/tablet.svg";
import Watch from "../assets/icons/clock.svg";
import Acessorios from "../assets/icons/headphones.svg";
import Mac from "../assets/icons/monitor.svg";

export default {
  name: "CategoryMenu",
  components: {
    Iphones,
    Ipad,
    Watch,
    Acessorios,
    Mac,
  },
  data() {
    return {
      categoriesList: [
        { label: "Iphones", icon: "Iphones", id: "iphones" },
        { label: "Ipad", icon: "Ipad", id: "ipad" },
        { label: "Watch", icon: "Watch", id: "watch" },
        { label: "Acessorios", icon: "Acessorios", id: "acessorios" },
        { label: "Mac", icon: "Mac", id: "mac" },
      ],
      selectedCategory: "iphones",
    };
  },
  methods: {
    onCategoryClick(id) {
      this.selectedCategory = id;
    },
    isActive(id) {
      return this.selectedCategory === id;
    },
  },
};
</script>

<style lang="less" scoped>
.category-menu {
  width: 130px;
  height: 100vh;
  background: @light-grey;

  display: flex;
  align-items: center;

  ul {
    list-style: none;
    padding: 0;
    width: 100%;

    li {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100px;

      p {
        margin-bottom: 0px;
        font-weight: 500;
        font-size: 14px;
        color: @write;
      }

      svg {
        stroke: @write;
      }

      &.active {
        background: @blue;
        border-radius: 8px;

        p {
          color: black;
        }

        svg {
          stroke: black;
        }
      }
    }
  }

  @media @tablets {
      width: 100%;
      height: fit-content;
      background: @bg-color;

      ul {
          display: flex;
          margin: 20px;  
          overflow: scroll;
          justify-content: center;

          li {
              min-width: 78px;
          }
      }
  }
}
</style>
