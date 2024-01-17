<template>
  <div>
    <StickyHeader />
    <div class="top">
      <div class="section">
        <div class="sortMethods">
          <div>
            <h4>최신순</h4> 
          </div>
          <div>
            <h4>인기순</h4>
          </div>
        </div>
        <hr>
      </div>
    </div>
    <div class="bottom">
      <div class="section">
        <div class="productsList">
          <div class="productArea" v-for="(product, index) in sampleProductsList.slice(0, render.showProductsCount)" v-bind:key="index">
            <div class="product" v-show="render.scrollY <= ((246 - 63 + render.productHeight + (parseInt((index + 3) / 3) - 1) * render.productHeight) + ((parseInt((index + 3) / 3) - 1) * render.productsGap) + (render.productHeight * 2)) && (render.scrollY + render.height) >= ((246 + (parseInt((index + 3) / 3) - 1) * render.productHeight) + ((parseInt((index + 3) / 3) - 1) * render.productsGap) - (render.productHeight * 2))">
              <div class="image">
                <img src="@/assets/images/dateImage.jpg">
              </div>
              <div class="description">
                <div>
                  <h5>{{ product.name }}</h5>
                </div>
                <div>
                  <h5>{{ product.price }}</h5>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="more" v-if="render.showProductsCount < sampleProductsList.length">
          <button @click="clickedMoreButton">
            <div>
              <h4>더보기</h4>
            </div>
            <div>
              <img src="@/assets/icons/downArrow.svg" width="20">
            </div>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import StickyHeader from '@/components/StickyHeader.vue'

export default {
  data() {
    return {
      sampleProductsList: [
        {
          name: 'perfume1',
          price: 1
        },
        {
          name: 'perfume2',
          price: 1
        },
        {
          name: 'perfume3',
          price: 1
        },
        {
          name: 'perfume4',
          price: 1
        },
        {
          name: 'perfume5',
          price: 1
        }
      ],
      render: {
        showProductsCount: (3 * 6),
        increaseShowProductsCount: (3 * 6),
        productHeight: 650,
        productsGap: 30,
        scrollY: 0,
        height: 0
      }
    }
  },
  components: {
    StickyHeader
  },
  mounted() {
    this.render.height = window.innerHeight;
    this.render.scrollY = window.scrollY;
    window.addEventListener('resize', this.resizing);
    window.addEventListener('scroll', this.scrolling);

    for (let i = 6; i <= 500; i++) {
      this.sampleProductsList.push({
        name: `perfume${i}`,
        price: 1
      });
    }
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resizing);
    window.removeEventListener('scroll', this.scrolling);
  },
  methods: {
    resizing() {
      this.render.height = window.innerHeight;
    },
    scrolling() {
      this.render.scrollY = window.scrollY;
    },
    clickedMoreButton() {
      this.render.showProductsCount = this.render.showProductsCount + this.render.increaseShowProductsCount;
    }
  }
}
</script>

<style lang="scss" scoped>
.top {
  padding: 0px 50px;
  padding-top: 163px;
  .section {
    display: flex;
    flex-direction: column;
    margin: 0px auto;
    max-width: 1200px;
    gap: 5px;
    .sortMethods {
      display: flex;
      gap: 10px;
      >* {
        cursor: pointer;
        display: flex;
        padding: 3px;
      }
      >*:hover {
        filter: invert(0.7);
      }
    }
    hr {
      border: none;
      border-top: 1px solid #dfdfdf;
    }
  }
}
.bottom {
  padding: 50px;
  .section {
    display: flex;
    flex-direction: column;
    margin: 0px auto;
    max-width: 1200px;
    .productsList {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-auto-rows: 650px;
      gap: 30px;
      .productArea {
        .product {
          cursor: pointer;
          display: flex;
          flex-direction: column;
          gap: 10px;
          .image {
            display: flex;
            height: 550px;
            border: 1px solid #f3f1f0;
            img {
              width: 100%;
              object-fit: cover;
            }
          }
          .description {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
          }
        }
      }
    }
    .more {
      display: flex;
      justify-content: center;
      button {
        cursor: pointer;
        display: flex;
        padding: 10px;
        border: 1px solid black;
        background-color: white;
        gap: 10px;
        outline: none;
        >* {
          display: flex;
          align-items: center;
          height: 100%;
        }
      }
    }
  }
}
</style>