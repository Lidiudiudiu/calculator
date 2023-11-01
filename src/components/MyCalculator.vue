<template>
     <div class="calculator black-mode" :class="{'white-mode':white_mode}">
        <!-- 计算器界面 -->
        <BarTop></BarTop>
        <!-- 一个只起美观作用的小图标 -->
        <SideNav></SideNav>
        <CalScreen></CalScreen >
        <!-- 显示屏幕 -->
        <CalButtons></CalButtons>
        <BarTop style="{padding-bottom: 0;}"></BarTop>
    </div>
</template>

<script>

import BarTop from './BarTop';
import SideNav from './SideNav';
import CalScreen from './CalScreen'
import CalButtons from './CalButtons'
export default {
  name: 'MyCalculator',
  data() {
    return {
        'white_mode':false,
        backgroundImage: ''
    }
  },
  methods: {
        changeBgd() {
            this['white_mode'] = !this['white_mode']
        }
  },
   mounted() {
        this.$bus.$on('changeBackground', this.changeBgd)
        
    },
  components:{
    BarTop,
    SideNav,
    CalScreen,
    CalButtons
  }
}
</script>

<style scoped>

.calculator {
    position: relative;
    height: 800px;
    width: 500px;
    background-color: rgba(0, 0, 0, 0.704);
    background-size: cover;
    border-radius: 5px 10px 10px 5px;
    transition: all 0.5s ease-in;
    overflow: hidden;
}


.calculator.white-mode {
    background-color: rgb(162 161 161);
    --primary-color: #fff;
    --secondary-color: #333;
}

.calculator.white-mode .buttons button {
    background-color: rgb(23, 21, 23);
}

.calculator.white-mode .buttons .function {
    background-color: #52514d7d;
    color: rgba(47, 255, 71, 0.434);
    }   

.calculator.white-mode .result {
    color: var(--secondary-color);
}

</style>
