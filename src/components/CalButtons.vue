<template>
  <div class="buttons">
        <button @click="clear" class="function">AC</button>
        <button @click="deleteFn" class="function btn-del">X</button>
        <button @click="calculateToggle" class="function" >±</button>
        <button @click="append('÷')" class="function">÷</button>
        <button @click="append(7)">7</button>
        <button @click="append(8)">8</button>
        <button @click="append(9)">9</button>
        <button @click="append('*')" class="function">*</button>
        <button @click="append(4)">4</button>
        <button @click="append(5)">5</button>
        <button @click="append(6)">6</button>
        <button @click="append('-')" class="function">-</button>
        <button @click="append(1)">1</button>
        <button @click="append(2)">2</button>
        <button @click="append(3)">3</button>
        <button @click="append('+')" class="function" >+</button>
        <button @click="calculatePercentage">%</button>
        <button @click="append(0)">0</button>
        <button @click="append('.')">.</button>
        <button @click="calculate" class="function">=</button>
    </div>
</template>


<script>
import pubsub from 'pubsub-js'
export default {
    name:'CalButtons',
    data() {
        return {
            equation: '0',  //等式结果是0
            isDecimalAdded: false,  //是否添加小数位，这是为了防止输入如两个小数点
            isOperatorAdded: false, //是否已经点击过运算符号 + — * /
            isStarted: false, //是否已经输入数据，在正负号和百分运算时有用
            classObj: {
                visible: false
            },
            bodyMode: {
                'white-mode': false
            }
        }
    },
    methods: {
        isOperator(character) {
            return ['+', '-', '*', '÷'].indexOf(character) > -1  //大于-1就代表已经有符号输入了
        },  //判断character是否为加，减，乘，除符号
        append(character) {
            if (this.equation === '0' && !this.isOperator(character)) {
                //当equation的值为零且输入不是符号时
                if (character === '.') {
                    this.equation += '' + character;
                    this.isDecimalAdded = true; //如果输入是‘.’，保留前面的0
                } else {
                    this.equation = '' + character;
                }
                this.isStarted = true; //数据已经输入
                this.sendEquation()
                return; //这个函式的代码结束
            }

            if (!this.isOperator(character)) {
                if (character === '.' && this.isDecimalAdded) {
                    return
                }//如果已经输入过.了，不允许继续输入.
                if (character === '.') {
                    this.isDecimalAdded = true;
                    this.isOperatorAdded = true;
                } else {
                    this.isOperatorAdded = false;
                }
                this.equation += '' + character
                this.sendEquation()
            }//如果输入是数字,处理小数点问题

            if (this.isOperator(character) && !this.isOperatorAdded) {
                this.equation += '' + character
                this.sendEquation()
                this.isDecimalAdded = false  //输入完运算符号后有输入'.'
                this.isOperatorAdded = true
            }//如果输入是符号，并且还防止连续输入符号

        },//点击加减乘除和小数位时
        calculate() {
            let result = this.equation.replace(new RegExp('x', 'g'), '*').replace(new RegExp('÷', 'g'), '/')
            this.equation = parseFloat(eval(result).toFixed(9)).toString();
            this.sendEquation()
            this.isDecimalAdded = false;
            this.isOperatorAdded = false;
        },//点击等号时计算结果
        calculateToggle() {
            if (this.isOperatorAdded || !this.isStarted) {
                return
            } //如果刚输入符号，或者没开始计算时禁用
            this.equation = this.equation + '* -1'
            this.calculate()
        },//点击正负号时
        calculatePercentage() {
            if (this.isOperatorAdded || !this.isStarted) {
                return
            }
            this.equation = this.equation + '*0.01'
            this.calculate()
        },//点击百分比符号时

        clear() {
            this.equation = '0'
            this.isDecimalAdded = false
            this.isOperatoradded = false
            this.isStarted = false
            this.sendEquation()
        },//点击AC号时,所有状态置于初始状态即可

        deleteFn() {
            if (this.equation.length === 0) {
                this.equation = '0';
            } else {
                this.equation = this.equation.slice(0, -1)
            }
            if (this.equation.length === 0) {
                this.equation = '0';
            }
            this.sendEquation()
        },//点击删除号时
        sendEquation() {
            pubsub.publish('getEquation',this.equation)
        }
    },
   
}
</script>

<style>
    .buttons {
    display: grid;
    grid-template-rows: repeat(5, 1fr);
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
    }

    .buttons button {
    width: 70px;
    height: 70px;
    font-size: 40px;
    font-family: Helvetica, sans-serif;
    border-radius: 50%;
    background-color: linear-gradient(135deg, rgba(230, 230, 230, 1) 0%, rgba(246, 246, 236, 1) 100%);
    box-shadow: -4px -4px 10px -8px rgba(255, 255, 255, 1), 4px 4px 10px -8px rgba(0, 0, 0, .3);
    color: #999;
    border: none;
    margin: 10px;
    }

    .buttons .function {
    background-color: #0a080194;
    color: rgba(47, 255, 71, 0.434);
    }   

    .buttons button:active {
    box-shadow: -4px -4px 10px -8px rgba(255, 255, 255, 1) inset, 4px 4px 10px -8px rgba(0, 0, 0, .3) inset;

    transform: scale(0.95);
    }

    .buttons button {
    background-color: lightgray;
    }
</style>