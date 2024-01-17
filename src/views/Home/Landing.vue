<template>
  <div>
    <StickyHeader />
    <div class="bannerArea">
      <!-- <Banner v-show="(render.scrollY + render.height) >= (0 - render.nodePadding + 63) && render.scrollY < (863 + render.nodePadding)" /> -->
      <Banner />
    </div>
    <div class="siteDescription">
      <img src="@/assets/imageIcons/aroma.svg" width="30px">
      <h3>이곳은 정말 개쩌는 향수만을 취급합니다.</h3>
    </div>
    <div class="mainArea">
      <div class="best">
        <div class="section">
          <!-- <div v-show="(render.scrollY + render.height) >= (863 + 70 - render.nodePadding + 63) && render.scrollY < (863 + 70 + 600 + render.nodePadding)"> -->
          <div>
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
      </div>
      <div class="set">
        <div class="section">
          <!-- <div v-show="(render.scrollY + render.height) >= (863 + 70 + 600 - render.nodePadding + 63) && render.scrollY < (863 + 70 + 600 + 800 + render.nodePadding)"> -->
          <div>
            <div class="sample">
              <div class="image">
                <img src="@/assets/images/perfumeSetImage.jpg">
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
      <div class="more">
        <div class="section">
          <!-- <div v-show="(render.scrollY + render.height) >= (863 + 70 + 600 + 800 - render.nodePadding + 63)"> -->
          <div>
            <div class="description">
              <div>
                <h1>More</h1>
              </div>
              <div>
                <h5>향수를 즐기는 다양한 방법</h5>
              </div>
              <hr>
            </div>
            <div class="sample">
              <div class="categories">
                <div class="category" v-for="(category, index) in categories" v-bind:key="index">
                  <div class="image">
                    <img :src="category.image">
                  </div>
                  <div class="inform">
                    <div>
                      <img :src="category.icon" width="50px">
                    </div>
                    <div>
                      <h5>{{ category.name }}</h5>
                    </div>
                  </div>
                </div>
              </div>
          </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="section">
        <div class="description">
          <h5>내가 만드는 중임</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StickyHeader from "@/components/StickyHeader.vue"
import Banner from "@/components/Banner.vue"

export default {
  data() {
    return {
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
      categories: [
        {
          name: "Shop",
          image: require("@/assets/images/shopImage.jpg"),
          icon: require("@/assets/imageIcons/shop.svg")
        },
        {
          name: "Gifts",
          image: require("@/assets/images/giftImage.jpg"),
          icon: require("@/assets/imageIcons/gift.svg")
        },
        {
          name: "Date",
          image: require("@/assets/images/dateImage.jpg"),
          icon: require("@/assets/imageIcons/date.svg")
        }
      ],
      render: {
        scrollY: 0,
        height: 0,
        nodePadding: 400
      }
    }
  },
  components: {
    StickyHeader,
    Banner
  },
  // mounted() {
  //   this.render.height = window.innerHeight;
  //   this.render.scrollY = window.scrollY;
  //   window.addEventListener("resize", this.resizing);
  //   window.addEventListener("scroll", this.scrolling);
  // },
  // beforeDestroy() {
  //   window.removeEventListener("resize", this.resizing);
  //   window.removeEventListener("scroll", this.scrolling);
  // },
  methods: {
    // resizing() {
    //   this.render.height = window.innerHeight;
    // },
    // scrolling() {
    //   this.render.scrollY = window.scrollY;
    // },
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
.bannerArea {
  height: 800px;
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
      max-width: 1200px;
      height: 500px;
      >div {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        height: 100%;
        gap: 10px;
      }
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
      max-width: 1200px;
      height: 700px;
      >div {
        display: flex;
        align-items: center;
        width: 100%;
        height: 100%;
        gap: 60px;
      }
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
  .more {
    padding: 50px 0px;
    .section {
      margin: 0px auto;
      max-width: 1200px;
      height: 752px;
      >div {
        display: flex;
        flex-direction: column;
        justify-content: center;
        width: 100%;
        height: 100%;
        gap: 30px;
      }
      .description {
        display: flex;
        flex-direction: column;
        text-align: center;
        gap: 30px;
        hr {
          border: none;
          border: 1px solid #f5f5f5;
        }
      }
      .sample {
        display: flex;
        justify-content: center;
        .categories {
          display: grid;
          grid-template-columns: repeat(3, 300px);
          grid-auto-rows: 600px;
          gap: 10px;
          .category {
            cursor: pointer;
            display: flex;
            flex-direction: column;
            height: 100%;
            gap: 20px;
            .image {
              display: flex;
              height: 100%;
              border: 1px solid #f3f1f0;
              img {
                width: 100%;
                object-fit: cover;
              }
            }
            .inform {
              display: flex;
              flex-direction: column;
              gap: 5px;
              * {
                display: flex;
                justify-content: center;
              }
            }
          }
        }
      }
    }
  }
}
.footer {
  padding: 50px 60px;
  background-color: #faf7ef;
  .section {
    margin: 0px auto;
    display: flex;
    flex-direction: column;
    max-width: 1200px;
  }
}
</style>