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
    <div class="siteDescription">
      <img src="@/assets/aroma.svg" width="30px">
      <h3>이곳은 정말 개쩌는 향수만을 취급합니다.</h3>
    </div>
    <div class="mainArea">
      <div class="best">
        <div class="section">
          <div class="description">
            <div>
              <h1>Best Sellers</h1>
            </div>
            <div>
              <h5>당신의 향긋한 일상을 함께할</h5>
              <h5>매 시즌 최고의 향수</h5>
            </div>
            <div>
              <button>Shop Best Sellers</button>
            </div>
          </div>
          <div class="sample">
            <div class="showMore">
              <div ref="leftArrow" class="leftArrow" @click="clickedLeftArrow">
                <img src="@/assets/icons/leftArrow.svg" width="20px">
              </div>
              <div ref="rightArrow" class="rightArrow" @click="clickedRightArrow">
                <img src="@/assets/icons/rightArrow.svg" width="20px">
              </div>
            </div>
            <div class="productList">
              <div ref="products" class="products">
                <div class="product" v-for="(product, index) in bestProducts.list" v-bind:key="index">
                  <div class="image">

                  </div>
                  <div class="inform">
                    <h5>{{ product.name }}</h5>
                    <h5>{{ product.price }}</h5>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="set">
        <div class="section">
          <div class="sample">
            <div class="image">
              <img src="@/assets/perfumeSet.jpg">
            </div>
          </div>
          <div class="description">
            <div>
              <h1>Set of Perfume</h1>
            </div>
            <div>
              <h5>다채로운 당신을 위한</h5>
              <h5>단 하나의 선택</h5>
            </div>
            <div>
              <button>Shop Set of Perfume</button>
            </div>
          </div>
        </div>
      </div>
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
      ],
      bestProducts: {
        showingProductsNum: 3,
        productWidth: 200,
        gap: 15,
        list: [
          {
            name: "perfume1",
            price: 20000,
            image: ""
          },
          {
            name: "perfume2",
            price: 10000,
            image: ""
          },
          {
            name: "perfume3",
            price: 15000,
            image: ""
          },
          {
            name: "perfume4",
            price: 50000,
            image: ""
          },
          {
            name: "perfume5",
            price: 8000,
            image: ""
          }
        ]
      },
    }
  },
  components: {
    Banner
  },
  methods: {
    clickedLeftArrow() {
      if (this.bestProducts.showingProductsNum === 3) return;
      const num = --this.bestProducts.showingProductsNum;

      const leftArrowElement = this.$refs["leftArrow"];
      const rightArrowElement = this.$refs["rightArrow"];
      const productsElement = this.$refs["products"];
      const width = this.bestProducts.productWidth + this.bestProducts.gap;
      const nextPositionX = (num - 3) * width;
      productsElement.style.transform = `translateX(-${nextPositionX}px)`;

      rightArrowElement.style.filter = "invert(0)";
      if (num === 3) leftArrowElement.style.filter = "invert(0.9)";
    },
    clickedRightArrow() {
      if (this.bestProducts.showingProductsNum === this.bestProducts.list.length) return;
      const num = ++this.bestProducts.showingProductsNum;

      const leftArrowElement = this.$refs["leftArrow"];
      const rightArrowElement = this.$refs["rightArrow"];
      const productsElement = this.$refs["products"];
      const width = this.bestProducts.productWidth + this.bestProducts.gap;
      const nextPositionX = (num - 3) * width;
      productsElement.style.transform = `translateX(-${nextPositionX}px)`;

      leftArrowElement.style.filter = "invert(0)";
      if (num === this.bestProducts.list.length) rightArrowElement.style.filter = "invert(0.9)";
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
.bannerArea {
  height: calc(100vh - 63px);
  max-height: 800px;
  padding-top: 63px;
}
.siteDescription {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 0px;
    color: white;
    background-color: #393d24;
    gap: 10px;
    img {
      filter: invert(1);
    }
  }
.mainArea {
  .best {
    padding: 50px 60px;
    .section {
      margin: 0px auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 1200px;
      height: 600px;
      gap: 10px;
    }
    .description {
      display: flex;
      flex-direction: column;
      gap: 30px;
      button {
        cursor: pointer;
        padding: 20px;
        border: 0px;
        font-weight: bold;
        color: white;
        background-color: black;
      }
      button:hover {
        filter: invert(0.3);
      }
    }
    .sample {
      display: flex;
      flex-direction: column;
      align-items: end;
      gap: 20px;
      .showMore {
        display: flex;
        gap: 14px;
        >* {
          cursor: pointer;
          user-select: none;
          display: flex;
          padding: 3px;
        }
        .leftArrow {
          filter: invert(0.9);
        }
      }
      .productList {
        position: relative;
        overflow: hidden;
        width: 630px;
        height: 350px;
        .products {
          position: absolute;
          display: grid;
          grid-auto-columns: 200px;
          grid-auto-rows: 350px;
          gap: 15px;
          transition: 300ms;
          .product {
            grid-row: 1;
            display: flex;
            flex-direction: column;
            width: 100%;
            gap: 5px;
            .image {
              display: flex;
              height: 100%;
              border: 1px solid #f3f1f0;
            }
            .inform {
              display: flex;
              flex-direction: column;
            }
          }
        }
      }
    }
  }
  .set {
    padding: 50px 60px;
    background-color: #eee9f2;
    .section {
      margin: 0px auto;
      display: flex;
      align-items: center;
      max-width: 1200px;
      height: 600px;
      gap: 60px;
    }
    .sample {
      width: 700px;
      height: 100%;
      .image {
        display: flex;
        height: calc(100% - 2px);
        border: 1px solid #f3f1f0;
        img {
          width: 100%;
          object-fit: cover;
        }
      }
    }
    .description {
      flex: 1;
      display: flex;
      flex-direction: column;
      gap: 30px;
      button {
        cursor: pointer;
        padding: 20px;
        border: 0px;
        font-weight: bold;
        background-color: transparent;
        border: 1px dashed black;
      }
      button:hover {
        filter: invert(0.8);
      }
    }
  }
}
</style>