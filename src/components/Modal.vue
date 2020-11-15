<template>
  <div class="outerWrapper">
      <div class="innerWrapper">
          <div class="photo">
            <img :src="photo"/>
          </div>
          <div class="description">
                <h2 class="title" > {{ title }}</h2>
                <p class="description">
                    {{ description }}
                </p>
          </div>
      </div>
    <div class="close"  @click="$emit('close-modal')">
    </div>
  </div>
 
</template>

<script>
export default {
    name: 'Modal',
    props:{
        item: {
            type: Object, 
            required: true,
        }
    },
    data(){
        return {
            photo: null,
            title: null,
            description: null
        };
    },
    mounted(){
        this.photo = this.item.links[0].href;
        this.title = this.item.data[0].title;
        this.description = this.item.data[0].description;
    }
}
</script>

<style lang="scss" scoped>

.outerWrapper{
    background-color: #f6f6f6;
    max-width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;

    @media(min-width: 1024px){
        max-width: 70%;
        height: 60%;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        box-shadow: 0 30px 30px -10px rgba(0,0,0,.3);
    }

}
.innerWrapper{
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content:center;
    align-items: center;
    flex-direction: column;

    .photo{
        width:90%;
        height:auto;
        background : #000;
    }

    img{
        width: 100%;
        height: 100%;
    }
    .description{
        margin-top: 10px;
        color: #333;
        padding : 15px;
        overflow: auto;
        max-height: 90%;
    }


    @media(min-width: 1024px){
        flex-direction : row;
        margin-right: 20px;

        .photo{
            min-width:50%;
            height:auto;
            background : #000;
        }
    }
}
.close{
    position:absolute;
    top:0px;
    right:0px;
    width:30px;
    height: 30px;
    padding:40px;
    cursor: pointer;

    &::before, 
    &::after {
        position:absolute;
        content : '';
        top:40px;
        right:20px;
        width: 30px;
        height: 3px;
        background: #000;
        display: block;
    }

     &::before{
      transform: rotate(45deg);   
     }
     
     &::after{
      transform: rotate(-45deg);   
     }
}
.title{
    color: #1e3d4a;
}



</style>