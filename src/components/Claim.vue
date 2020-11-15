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
        
    }
    
    .subclaim{
        margin: 25px 0 0 0;
        font-size: 30px;
    }


</style>