<template>
  <div class="about">
    <h1>{{lang}}{{$route.params.id}}</h1>
  </div>
</template>
<script>
export default {
   props:['lang'],
   created(){
      console.log(this.lang);
      console.log(this.$route);
      
      
   }
}
</script>