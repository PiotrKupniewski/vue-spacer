<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <p class="logo" v-if="step === 1">SPACER</p>
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
    />
    <div class="imageResults" v-if="results && !loading && step == 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="openModal(item)"
      />
    </div>
    <div class="loader" v-if="step === 1 && loading"></div>
    <Modal
      v-if="modalOpen"
      @close-modal="modalOpen = false"
      :item="modalItem"
    />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from './components/Claim.vue';
import SearchInput from './components/SearchInput.vue';
import HeroImage from './components/HeroImage.vue';
import Item from './components/Item.vue';
import Modal from './components/Modal.vue';

const API = 'https://images-api.nasa.gov/';

export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      this.step = 1;
      axios
        .get(`${API}search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
    openModal(item) {
      this.modalItem = item;
      this.modalOpen = true;
    },
  },
};
</script>
<style lang="scss" >
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

body {
  font-family: 'Montserrat', sans-serif;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3 ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.3 ease;
}

.slide-enter,
.slide-leave-to {
  margin-top: 30px;
}

.wrapper {
  min-height: 100vh;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100vw;
  height: 100vh;

  &.flexStart {
    justify-content: flex-start;
  }
}

.imageResults {
  margin-top: 50px;
  width: 80%;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 20px;

  @media (min-width: 768px) {
    grid-template-columns: repeat(3, 1fr);
  }
}

.logo {
  position: absolute;
  top: 60px;
  color: black;
  font-size: 25px;
}

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 80px;
  height: 80px;
}

.loader:after {
  content: ' ';
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s linear infinite;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
