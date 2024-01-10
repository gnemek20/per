<template>
  <div>
    <div class="stickyHeader">
      <div class="menu">
        <div v-for="(menu, index) in menuItems" v-bind:key="index">
          <h5>{{ menu.name }}</h5>
        </div>
      </div>
      <div class="title">
        <h1>Title</h1>
      </div>
      <div class="option">
        <div v-for="(option, index) in optionItems" v-bind:key="index">
          <h5>{{ option.name }}</h5>
        </div>
      </div>
    </div>
    <div class="bannerArea">
      <Banner />
    </div>
  </div>
</template>

<script>
import Banner from "@/components/Banner.vue"

export default {
  data() {
    return {
      menuItems: [
        {
          name: "Shop"
        },
        {
          name: "Our Story"
        },
        {
          name: "Get in Touch"
        },
        {
          name: "Gallery"
        }
      ],
      optionItems: [
        {
          name: "Cart"
        },
        {
          name: "Steamed"
        }
      ]
    }
  },
  components: {
    Banner
  }
}
</script>

<style lang="scss" scoped>
.stickyHeader {
  z-index: 1;
  position: fixed;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: calc(100% - 40px);
  padding: 10px 20px;
  background-color: #faf7ef;
  * {
    display: flex;
    align-items: center;
    gap: 30px;
  }
  .menu {
    div {
      cursor: pointer;
      display: flex;
      padding: 10px;
    }
  }
  .title {
    justify-content: center;
  }
  .option {
    justify-content: end;
    div {
      cursor: pointer;
      display: flex;
      padding: 10px;
    }
  }
}
.bannerArea {
  height: calc(100vh - 63px);
  max-height: 700px;
  padding-top: 63px;
}
</style>