<template>
  <div class="book-slider">
    <div class="book-slider__content">
      <div class="book-slider__photo">
        <div
          class="book-slider__track"
          :style="{
            transform: `translate3d(${getCurrentPosition}px, 0px, 0px)`,
          }"
        >
          <div
            class="book-slider__item"
            v-for="item in projects"
            :key="item.id"
          >
            <img :src="`../public/${item.photo}`" alt="" />
            <div class="book-slider__overlay"></div>
            <a
              target="_blank"
              :href="projects[activeItemId - 1].link"
              class="book-slider__loupe"
            >
              <img src="../assets/images/icons/loupe.svg" alt="" />
            </a>
          </div>
        </div>
      </div>
      <div class="book-slider__info">
        <div class="book-slider__header">
          <h3 class="book-slider__title">
            {{ projects[activeItemId - 1].title }}
          </h3>
          <div class="book-slider__navigation">
            <div
              :class="`book-slider__point ${
                number == activeItemId ? 'active' : ''
              }`"
              v-for="number in projects.length"
              :key="number"
              @click="slide(number)"
            ></div>
          </div>
        </div>
        <p class="book-slider__text">
          {{ projects[activeItemId - 1].desctiption }}
        </p>
      </div>
    </div>
    <div class="book-slider__buttons">
      <a
        target="_blank"
        :href="projects[activeItemId - 1].link"
        class="button button_white"
        >Go to website</a
      >
      <router-link to="contacts" class="button"
        >Let`s work together</router-link
      >
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      projects: [
        {
          id: 1,
          title: "Pravoe delo",
          desctiption:
            '"Pravoe delo" is a law company that has been active on the Russian market for about 10 years and processes many applications on a daily basis. I worked in this company as a Frontend Developer on Vue.js.',
          photo: "pravoe_delo.png",
          link: "https://pravoe-delo.su",
        },
        {
          id: 2,
          title: "Weather",
          desctiption:
            "A simple one-page website that shows accurate weather anywhere in the world. The site is made in Nuxt.js.",
          photo: "weather.png",
          link: "https://main--weatheraroundworld.netlify.app",
        },
        {
          id: 3,
          title: "Crappo",
          desctiption:
            "Krappo is an adaptive one-page website about cryptovolut. The site was made as a pet project.",
          photo: "crappo.png",
          link: "http://z90930xn.beget.tech",
        },
        {
          id: 4,
          title: "Deluxe house",
          desctiption:
            "Luxury Home is a design studio website. Multi-page, adaptive and cross-browser. The site has been converted to wordpress. Made as a pet project.",
          photo: "deluxe_house.png",
          link: "http://i98248bv.beget.tech",
        },
        {
          id: 5,
          title: "Qpick Shop",
          desctiption:
            "Qpick store is a multi-page online store for Apple products in Vue.js. The site was made as a pet project.",
          photo: "qpick.png",
          link: "https://qpickshop.netlify.app",
        },
      ],
      activeItemId: 1,
      currentPosition: 0,
    };
  },
  computed: {
    getCurrentPosition() {
      return this.currentPosition;
    },
  },
  mounted() {},
  methods: {
    slide(number) {
      this.currentPosition = -(
        (number - 1) *
        (document.querySelector(".book-slider__item").offsetWidth + 20)
      );
      this.activeItemId = number;
    },
  },
};
</script> 