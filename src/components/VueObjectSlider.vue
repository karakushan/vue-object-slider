<template>
  <div class="object-slider">
    <button @click.prevent="prev()"
            :class="{'object-slider__prev':true, 'object-slider__nav':true, disabled:prevDisabled}"
    ><i
        class="ef ef-keyboard-arrow-left"></i></button>
    <button @click.prevent="next()"
            :class="{'object-slider__next':true, 'object-slider__nav':true,disabled: nextDisabled}"
    ><i
        class="ef ef-keyboard-arrow-right"></i></button>
    <div class="object-slider__container" ref="container">
      <div class="object-slider__viewport" :style="{
      'transform': 'translateX('+translateX+'px)',
       'transition': 'transform 0.2s ease-in-out 0s'
    }" ref="viewport">
        <div class="object-slider__slide"
             v-for="(item,key) in items" :key="key"
             :style="{'min-width':item_width+'px','padding-right':gap+'px'}"
        >
          <div class="object-slider__card">
            <div class="object-slider__slider" v-if="item.images.length">
              <button class="object-slider__slider-arrow object-slider__slider-prev" @click.prevent="thumbPrev(item)">
                <i class="ef ef-keyboard-arrow-left search-slider__button-icon"></i>
              </button>
              <button class="object-slider__slider-arrow object-slider__slider-next" @click.prevent="thumbNext(item)">
                <i class="ef ef-keyboard-arrow-right search-slider__button-icon"></i>
              </button>
              <a href="#" :class="{fade:item.slideTransition}">
              <span class="object-slider__blur"
                    :style="{'background-image':'linear-gradient(0deg, rgba(255, 255, 255, 0.4), rgba(255, 255, 255, 0.4)), url('+item.images[item.thumb]+')'}">

              </span>
                <img :src="item.images[item.thumb]" alt="">
                <span class="object-slider__slide-count">{{ item.thumb + 1}}/{{ item.images.length }}</span>
              </a>
            </div>
            <div class="object-slider__body">
              <div class="object-slider__top">
                <div class="object-slider__price">{{ item.price }} BYN</div>
                <div class="object-slider__price-m">{{ item.price }} BYN/<span>м<sup>2</sup></span></div>
                <button class="object-slider__btn-wishlist">
                  <div class="object-slider__tooltip"><span class="description">Добавить в избранное</span></div>
                  <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="1.5rem" height="1.5rem"
                       fill="currentColor">
                    <path
                        d="M13.3536 20.1307C12.5936 20.8207 11.4236 20.8207 10.6636 20.1207L10.5536 20.0207C5.30357 15.2707 1.87357 12.1607 2.00357 8.28065C2.06357 6.58065 2.93357 4.95065 4.34357 3.99065C6.98357 2.19065 10.2436 3.03065 12.0036 5.09065C13.7636 3.03065 17.0236 2.18065 19.6636 3.99065C21.0736 4.95065 21.9436 6.58065 22.0036 8.28065C22.1436 12.1607 18.7036 15.2707 13.4536 20.0407L13.3536 20.1307Z"></path>
                  </svg>
                </button>
              </div>
              <div class="object-slider__params">
                <span><a href="#">3-комн. квартира</a></span>
                <span>72.5 м<sup>2</sup></span>
                <span>1/5 эт.</span>
              </div>
              <div class="object-slider__row"><a class="non-click" href="#">ул. Полиграфический 1-й пер., </a> д. 4
              </div>
              <div class="object-slider__row object-slider__metro">
                <span><i class="ef ef-metro"></i></span>
                <span><a class="non-click" href="#">Кунцевщина</a> <span
                    class="object-slider__metro-time">0 мин.<i class="ef ef-walk"></i></span></span>
              </div>
              <div class="object-slider__bottom">
                <button><i class="ef ef-phone"></i> Показать телефон</button>
                <div class="object-slider__contact" style="display: none;">
                  <img :src="item.agent.avatar" alt="Avatar">
                  <div class="object-slider__contact-meta">
                    <a href="#" class="object-slider__contact-tel">{{ item.agent.phone }}</a>
                    <div class="object-slider__contact-name">{{ item.agent.fullName }}</div>
                  </div>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

import $ from 'jquery'

export default {
  name: "VueObjectSlider",
  data() {
    return {
      translateX: 0,
      viewportWidth: 0,
      activeSlide: 1
    }
  },

  props: {
    items: {
      type: Array,
      default() {
        return [
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },
          {
            price: '359625',
            priceArea: '4960 ',
            room: 3,
            area: 75,
            floor: 1,
            floorTotal: 5,
            slideTransition:false,
            address: 'Советский, ул. Полиграфический 1-й пер., д. 4',
            agent: {
              avatar: 'https://cdn.esoft.digital/240320/media/profiles/7b/32/392dd75e387714b8a57095106b7012a5d7dc388c.jpg',
              fullName: 'Шалковская Ольга',
              phone: '+375 44 508-97-59'
            },
            thumb: 0,
            images: [
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
              'https://cdn.esoft.digital/320240/photos/266030d2e6d6ab5988f0ab1edf25e539e4862ef8.jpg',
            ]
          },


        ]
      }
    },

    item_width: {
      type: Number,
      default() {
        return 365;
      }
    },
    gap: {
      type: Number,
      default() {
        return 20;
      }
    }
  },
  computed: {
    containerWidth() {
      return this.item_width * this.items.length
    },
    prevDisabled() {
      return this.translateX >= 0
    },
    nextDisabled() {
      return this.activeSlide > this.items.length - 3
    }
  },
  mounted() {
    let ref = this.$refs['container']
    this.viewportWidth = ref.clientWidth
    $(document).on('click', '.object-slider__bottom button', function () {
      $(this).hide().next().show()
    });
  },
  methods: {
    thumbNext(item) {
      item.slideTransition = true
      setTimeout(() => {
        if (item.thumb == item.images.length - 1) {
          item.thumb = 0
        } else {
          item.thumb++
        }
        item.slideTransition = false
      }, 200)


    },
    thumbPrev(item) {
      item.slideTransition = true
      setTimeout(() => {
        if (item.thumb == 0) {
          item.thumb = item.images.length - 1
        } else {
          item.thumb--
        }
        item.slideTransition = false
      }, 200)

    },
    next() {


      // if (this.activeSlide==10){
      //   this.translateX = this.translateX - 51
      // }else{
      //   this.translateX = this.translateX - this.item_width
      // }
      if (this.activeSlide <= this.items.length - 3) {
        this.activeSlide++
        this.translateX = this.translateX - this.item_width
      }


    },
    prev() {
      if (this.translateX < 0) {
        this.activeSlide--

        this.translateX = this.translateX + this.item_width
      }

    }
  }
}
</script>

<style lang="scss" scoped>
@import "../style";

</style>