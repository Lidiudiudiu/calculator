<template>
  <div class="nav" :class="{visible : navVisble}">
        <ul>
            <li> <button @click="changeBgd" class="mode-button" >
                <span class="font-icon">{{ bodyMode['white-mode'] ? '' : '' }}</span>
                <span class="font">{{ bodyMode['white-mode'] ? 'dark mode' : 'light mode' }}</span>
            </button></li>
            <li>
            <button  class="bgd-button" ></button>
            </li>
            <li>
                <button class="change-bgd-button">
                    <span @click="changeBgdImageLess" class="left"></span>
                    切换背景图片
                    <span @click="changeBgdImageAdd" class="right"></span>
                </button>
            </li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
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
            currentImage: 0
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
    transform: translateX(-100%);
    transition: all 0.3s;
}

.visible {
    transform: translateX(0);
    transition: all 0.3s;
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

.nav .bgd-button {
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