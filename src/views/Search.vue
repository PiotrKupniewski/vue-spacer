<template>
  <div class="wrapper">
      <Claim/>
      <SearchInput/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '../components/Claim';
import SearchInput from '../components/SearchInput';

const API  = 'https://images-api.nasa.gov/';

export default {
    name : 'Search',
    components: {
        Claim,SearchInput
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

<style lang="scss" scoped >
    .wrapper{
        display: flex;
        flex-direction: column;
        align-items : center;
        margin: 0;
        padding: 30px;
        width: 100%;
    }

    .search{
        display: flex;
        flex-direction: column;
        width: 300px;

        label{
            font-family:Montserrat, sans-serif;
        }


        input{
            height: 30px;
            border:0;
            border-bottom:  1px solid black;
        }

    }
</style>