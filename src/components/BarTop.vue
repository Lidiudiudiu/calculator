<template>
  <div class="bar">
    <span></span>
  </div>
</template>

<script>
export default {
    name:'BarTop'
}
</script>

<style scoped>
    .bar {
    display: flex;
    justify-content: center;
    padding-top: 20px;
    }

    .bar span {
    height: 2px;
    width: 110px;
    background-color: #fff;
    }

</style>