<template>
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
</template>

<script>
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
      ],
    }
  }
}
</script>

<style lang="scss" scoped>
.stickyHeader {
  z-index: 1;
  position: fixed;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: calc(100% - 100px);
  padding: 10px 50px;
  background-color: #faf7ef;
  * {
    display: flex;
    align-items: center;
  }
  .menu {
    gap: 30px;
    div {
      cursor: pointer;
      display: flex;
      padding: 10px;
    }
    div:hover {
      filter: invert(0.7);
    }
  }
  .title {
    justify-content: center;
  }
  .option {
    justify-content: end;
    gap: 30px;
    div {
      cursor: pointer;
      display: flex;
      padding: 10px;
    }
    div:hover {
      filter: invert(0.7);
    }
  }
}
</style>