<template>
    <div class="product-images-popup">
        <div class="product-images-popup-modal">
            <div class="product-images-popup-header">

            </div>

            <div class="product-images-popup-body">
                <div class="product-images-popup-carousel_wrap">
                    <transition-group tag="div" class="product-images-popup-carousel">
                        <div
                                v-for="(imgUrl) in testImgs"
                                :key="imgUrl"
                                class="product-images-popup-slide"
                        >
                            <div v-touch:swipe.left="onSwipeLeft">
                                <div v-touch:swipe.right="onSwipeRight">
                                    <img v-bind:src="imgUrl" />
                                </div>
                            </div>
                        </div>
                    </transition-group>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  import Vue from 'vue'
  import Vue2TouchEvents from 'vue2-touch-events'
  Vue.use(Vue2TouchEvents)

  export default {
    name: 'PopUpCarousel',

    components: {

    },

    props: ['imagesProp'],

    data() {
      return {
        //images: Vue.util.extend({}, JSON.parse(this.imagesProp.textContent)),
        testImgs: [
          "//cdn.shopify.com/s/files/1/0131/9514/9369/products/redpixie_small.jpg?v=1539581610",
          "//cdn.shopify.com/s/files/1/0131/9514/9369/products/pixieside_small.jpg?v=1539581610",
          "//cdn.shopify.com/s/files/1/0131/9514/9369/products/pixieback_574f736f-f149-4349-a55c-8acdc41639b7_small.jpg?v=1539581610",
          "//cdn.shopify.com/s/files/1/0131/9514/9369/products/redpixie_332adf42-cae3-40c8-b820-63223ccde0e9_small.jpg?v=1539581610"
        ]
      }
    },

    // compute
    computed: {

    },

    methods: {
      onSwipeLeft () {
        console.log('left')
        const last = this.testImgs.pop()
        this.testImgs = [last].concat(this.testImgs)

        // test
        //console.log('-- test --')
        //console.log(this.testImgs)
      },

      onSwipeRight () {
        console.log('right');
        const first = this.testImgs.shift()
        this.testImgs = this.testImgs.concat(first)

        // test
        //console.log('-- test --')
        //console.log(this.testImgs)
      }
    },
    mounted() {
      //console.log(JSON.stringify(images.textContent, null, 4));
      //this.images = Object.assign({}, JSON.parse(this.imagesProp.textContent))
    }
  };
</script>

<style>
    .product-images-popup {
        position: fixed;
        z-index: 100;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background: #fff;
        transition: opacity .25s ease-in-out;
    }

    .product-images-popup-modal {

    }

    .product-images-popup-carousel_wrap {
        display: flex;
        /* top to bottom */
        flex-direction: column;
        /* center carousel */
        align-items: center;
    }

    .product-images-popup-carousel {
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;

        width: 24em;
        min-height: 25em;
    }

    .product-images-popup-slide {
        /*grow, shrink, basis*/
        flex: 0 0 20em;
        height: 20em;
        margin: 1em 1em 1em 1em;

        display: flex;
        justify-content: center;
        align-items: center;

        border: 0.1em solid #000;

        /* transition */
        transition: transform 0.3s ease-in-out;
    }

    .product-images-popup-slide:first-of-type {
        opacity: 0;
    }

    .product-images-popup-slide:last-of-type {
        opacity: 0;
    }
</style>
