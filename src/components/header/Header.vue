<template>
  <div>{{poiInfo.name}}</div>
</template>

<script>
  export default {
    props:{
      poiInfo:{
        type:Object,
        default:{}
      }
    }
  }
</script>

<style scoped>

</style>
