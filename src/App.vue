<template>
  <div :class="[{ flexStart : step === 1 } , 'wrapper']">
    <transition name="slide">
      <p class="logo" v-if="step === 1"> SPACER </p>
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput"
    :dark="step === 1" />
    <div class="imageReults" v-for="item in results" :key="item.data.nasa_id">
      <ul>
        <li>
          {{ item.links[0].href}}
        </li>
      </ul>
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from './components/Claim';
import SearchInput from './components/SearchInput';
import HeroImage from './components/HeroImage';

const API  = 'https://images-api.nasa.gov/';

export default {
    name : 'App',
    components: {
        Claim,SearchInput,HeroImage
    },
    data(){
        return {
          loading :false, 
          step : 0,
          searchValue : '',
          results : [],
        }
    },
    methods: {
        handleInput: debounce( function(){
          this.loading = true;
          this.step = 1;
          axios.get(`${API}search?q=${this.searchValue}&media_type=image`)
          .then((response) => {
              this.results = response.data.collection.items;
              this.loading = false;
              this.step = 1;
          })
          .catch((error) => {
              console.log(error);
          });
      }, 500),
    }
};
</script>
<style lang="scss" >

  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

  * {
    box-sizing : border-box;
    margin: 0;
    padding: 0 ;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-rendering: optimizeLegibility;
  }

  body{
    font-family: 'Montserrat', sans-serif;
  }
  
  .fade-enter-active, .fade-leave-active{
    transition: opacity .3 ease;
  }

  .fade-enter, .fade-leave-to{
    opacity:0;
  }

  .slide-enter-active, .slide-leave-active{
    transition: margin-top .3 ease;
  }

  .slide-enter, .slide-leave-to{
    margin-top: 30px;
  }

  .wrapper{
    min-height: 100vh;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items : center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100vw;
    height:100vh;

    &.flexStart{
      justify-content:flex-start;
    }
  }

  .logo{
    position: absolute;
    top:60px;
    color: black;
    font-size:25px;
  }
</style>
