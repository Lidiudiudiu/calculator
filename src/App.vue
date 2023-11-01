<template>
  <div>
    <MyCalculator></MyCalculator>
  </div>
</template>

<script>
import MyCalculator from './components/MyCalculator'
export default {
    name:'App',
    components: {
      MyCalculator
    }
}
</script>

<style>
  @font-face {
    font-family: 'icomoon';
    src: url('fonts/icomoon.eot?tc7q2y');
    src: url('fonts/icomoon.eot?tc7q2y#iefix') format('embedded-opentype'),
        url('fonts/icomoon.ttf?tc7q2y') format('truetype'),
        url('fonts/icomoon.woff?tc7q2y') format('woff'),
        url('fonts/icomoon.svg?tc7q2y#icomoon') format('svg');
    font-weight: normal;
    font-style: normal;
    font-display: block;
}

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

:root {
    --primary-color: #000;
    --secondary-color: #fff;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: linear-gradient(to left bottom, #d16ba5, #c777b9, #ba83ca, #aa8fd8, #9a9ae1, #8aa7ec, #79b3f4, #69bff8, #52cffe, #41dfff, #46eefa, #5ffbf1);
    height: 100vh;
    width: 100vw;
    overflow: hidden;
    margin: 0 auto;
  
}

</style>