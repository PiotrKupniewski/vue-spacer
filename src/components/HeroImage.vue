<template>
  <div class="heroImage"></div>
</template>

<script>
export default {
    name : 'HeroImage',
}
</script>

<style >
    .heroImage{
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        z-index : -1;
        background-image: url(../assets/background-cosmos.jpg);
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 90% 0%;
    }

    .heroImage::after{
        content : '';
        background: rgba(0,0,0,0.1);
        position: absolute;
        top: 0;
        left: 0;
        z-index: 1;
        width:100%;
        height:100vh;
    }
</style>