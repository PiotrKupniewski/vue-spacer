<template>
 <div class="claimWrapper"> 
  <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Start your joruney through our amazing galaxy, and discover places you neve event heard of
    </p>
    <p class="subclaim">
        Type anything space-related
    </p>
 </div> 
</template>

<script>
export default {
    name: 'Claim',
}


</script>

<style >
    .claimWrapper{
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: #fff;
    }

    .claim{
        font-size: 140px;
        font-weight: 700;;
        margin: 0;

        @media(min-wdith: 768px){
            font-size : 200px;
        }   
    }
    
    .subclaim{
        margin: 25px 0 0 0;
        font-size: 40px;
        font-weight: 300;
     

        @media(min-wdith: 768px){
            font-size : 60px;
            line-height: 1;
            width: 700px;
            letter-spacing : 2px;
        } 
    }


</style>