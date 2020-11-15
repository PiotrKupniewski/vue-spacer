<template>
  <div class="wrapper">
      <HeroImage/>
      <Claim/>
      <SearchInput v-model="searchValue" @input="handleInput()"/>
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
            searchValue : '',
            results : [],
        }
    },
    methods: {
        handleInput: debounce( function(){
            axios.get(`${API}search?q=${this.searchValue}&media_type=image`)
            .then((response) => {
                this.results = response.data.collection.items;
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

  .wrapper{
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items : center;
    justify-content: center;
    margin: 0;
    padding: 30px;
    width: 100vw;
    height:100vh;
    

    }
</style>
