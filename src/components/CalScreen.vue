<template>
  <div class="screen" :style="{ 'background-image': 'url(' + backgroundImage + ')' }">
        <button @click="changeNav" class="nav-button open-button" ></button>
        <div class="result" >
            {{ equation.replace('**', '∧') }}
        </div>
    </div>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
    name:'CalScreen',
    data() {
        return {
            equation: '0',
            navVisible: false,
            backgroundImages: [
                require('../../public/images/card1.jpg'),
                require('../../public/images/card2.jpg'),
                require('../../public/images/card3.jpg'),
                require('../../public/images/card4.jpg'),
                require('../../public/images/card5.jpg'),
                require('../../public/images/card6.webp'),
                require('../../public/images/card7.png'),
                require('../../public/images/card8.jpg'),
                require('../../public/images/card9.jpg'),
                require('../../public/images/card10.jpg'),
                require('../../public/images/card11.png'),
                require('../../public/images/card12.webp'),
               
            ],
           cImage:0,
           
        }
    },
    computed: {
        backgroundImage() {
            return this.backgroundImages[this.cImage];
        }
    },
    methods: {
        getData(_,data) {
            this.equation = data
        },
        changeNav(){
            this.navVisible = !this.navVisible
            this.$bus.$emit('changeVisible',this.navVisible)
        },
        cutImage(imageNum) {
            this.cImage = imageNum
        },
        
    },
   
    mounted() {
       pubsub.subscribe('getEquation',this.getData)
       this.$bus.$on('changeBackgroundImage',this.cutImage)
       
    },
    beforeDestroy() {
         pubsub.unsubscribe('getEquation');
    }
}
</script>

<style>
    .screen {
    position: relative;
    height: 240px;
    display: flex;
    color: #fff;
    font-size: 40px;
    flex-direction: column;
    align-items: flex-end;
    padding-right: 20px;
    padding-top: 40px;
    overflow: hidden;
    background-image: url(../../public/images/card1.jpg);
    background-size: cover;
    }
    .result {
    text-align: right;
    line-height: 1em;
    font-size: 48px;
    padding: 0 20px;
    color:#fff;
    }
    .nav-button {
    position: absolute;
    top: 7px;
    left: 5px;
    font-family: icomoon;
    border: none;
    background-color: transparent;
    cursor: pointer;
    z-index: 2;
    font-size: 29px;
    color: #bf86c6;
    }

    .nav-button:active {
        transform: scale(0.98);
    }

</style>