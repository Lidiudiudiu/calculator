<template>
  <transition name="nav">
    <div v-show="navVisble" class="nav">
        <ul>
            <li> <button @click="changeBgd" class="mode-button" >
                <span class="font-icon">{{ bodyMode['white-mode'] ? '' : '' }}</span>
                <span class="font">{{ bodyMode['white-mode'] ? 'dark mode' : 'light mode' }}</span>
            </button></li>
            <li>n
            <button @click="changeSound" class="voice-turn-button" :style="{ 'background-color': backgroundColor[currentSound] }"><span class="font-change"></span> Change Keyvoice</button>
            </li>
            <li>
                <button class="change-bgd-button">
                    <span @click="changeBgdImageLess" class="left"></span>
                    Change Image
                    <span @click="changeBgdImageAdd" class="right"></span>
                </button>
            </li>
            <li>
               <button @click="changeOpen" class="is-sound-button" >
                <span class="font-icon">{{ keypodTone.isopen ? '' : '' }}</span>
                <span class="font">{{ keypodTone.isopen ? 'close sounds' : 'open sounds' }}</span>
               </button>
            </li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
  </transition>
</template>

<script>

export default {
    name:'SideNav',
    data() {
        return {
            navVisble: false,
            bodyMode: {
                'white-mode': false
            },
            keypodTone: {
                isopen:true
            },
            backgroundColor: [
                '#5856dd','red','pink','blue'
            ],
            currentImage: 0,
            currentSound: 0
        }
    },
    methods: {
        changeNav(d) {
            this.navVisble = d
        },
        changeBgd() {
            this.bodyMode['white-mode'] = !this.bodyMode['white-mode']
            this.$bus.$emit('changeBackground', this.bodyMode['white-mode'])
        },
       changeBgdImageAdd() {
            this.currentImage++
            if(this.currentImage == 12) this.currentImage=0
            this.$bus.$emit('changeBackgroundImage', this.currentImage)
       },
       changeBgdImageLess() {
           this.currentImage--
            if (this.currentImage == -1) this.currentImage = 11
            this.$bus.$emit('changeBackgroundImage', this.currentImage)
        },
        changeSound() {
            if(this.currentSound == 3) this.currentSound = 0;
            else this.currentSound++;
            this.$bus.$emit('changeKeypod',this.currentSound)
        },
        changeOpen(){
            this.keypodTone.isopen = !this.keypodTone.isopen;
            this.$bus.$emit('changeSoundOpen', this.keypodTone.isopen)
        }
    },
    mounted() {
        this.$bus.$on('changeVisible',this.changeNav)
    }
}
</script>

<style scoped>
    .nav {
    position: absolute;
    /* display: flex;
    flex-direction: column; */
    top: 0;
    left: 0;
    width: 210px;
    height: 100vh;
    z-index: 1;
    background-color: rgba(16, 12, 12, 0.976);
    transition: all 0.3s;
}

.nav-enter,
.nav-leave-to {
    transform: translateX(-100%);
}

/* 进入的过程、离开的过程 */
.nav-enter-active,
.nav-leave-active {
    transition: 1.5s ease;
}

/* 进入的终点、离开的起点 */
.nav-enter-to,
.nav-leave {
    transform: translateX(0);
}



.nav .font-icon {
    font-family: icomoon;
    position: absolute;
    left: 10px;
    top: 30%;
}

.nav .font {
    position: absolute;
    right: 10px;
    top: 25%;
}

.nav button {
     position: absolute;
    right: 0px;
    cursor: pointer;
    font-size: 20px;
    border: 0;
    border-radius: 4px;
    width: 100%;
    height: 40px;
}

.nav .mode-button {
    top: 66px;
    color: var(--secondary-color);
    background-color: var(--primary-color);
}

.nav .voice-turn-button {
    font-family: icomoon;
    top: 106px;
    background-color: #5856dd;
}

.change-bgd-button {
    position: relative;
    text-align: center;
    line-height: 0.8em;
    color: #000;
    font-size: 17px;
    font-weight: 600;
    top: 146px;
    background-color: #e6df13;
}

.change-bgd-button span {
  display: flex;  
  width: 40px;
  height: 30px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-family: icomoon;
  justify-content: center;
  align-items: center;
  color: purple;
}

.change-bgd-button span:active {
    opacity: 0.8;
}

.change-bgd-button .left {
  left: 5px;
}

.change-bgd-button .right {
  right: 5px;
}

.is-sound-button {
    font-family: icomoon;
    line-height: 18px;
    color: #11100a;
    top: 186px;
    background-color: #31c93491;
}

.is-sound-button .font-icon {
    color: pink;
}

.nav button:focus {
    outline: none;
}

.nav button:active {
    transform: scale(0.95);
}

.nav .change-bgd-button:active {
    transform: scale(1);
}
</style>