<template>
    <div>
        <div v-if="step===0" class="intro">请输入你的问题，并按下回车</div>
        <input v-if="step===0" class="input" v-model="inputValue" @keyup.enter="handleEnter">

        <div v-if="step===1">
            <div class="title">{{ displayValue }}</div>
            <button class="btn confirm" @mouseenter="swapText('是的！')" @mouseleave="swapBack" @click="this.step=2">
                {{ button1Text }}
            </button>
            <button class="btn cancel" @mouseenter="swapText('不是~')" @mouseleave="swapBack" @click="this.step=2">
                {{ button2Text }}
            </button>
            <button v-if="thinkShow[0]" class="think think1" @mouseenter="changeThink">我再想想</button>
            <button v-if="thinkShow[1]" class="think think2" @mouseenter="changeThink">我再想想</button>
            <button v-if="thinkShow[2]" class="think think3" @mouseenter="changeThink">我再想想</button>
            <button v-if="thinkShow[3]" class="think think4" @mouseenter="changeThink">我再想想</button>
        </div>

        <div v-if="step === 2" class="end">果然，你就承认吧</div>

        <div v-if="mobileTip" class="mobile">
            建议使用电脑打开，才有鼠标悬停效果哦~
            <button @click="mobileTip=false">ok</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            button1Text: '是的！',
            button2Text: '不是~',
            inputValue: '',
            step: 0,
            displayValue: '',
            thinkShow: [0,0,0,1],
            mobileTip: true,
        }
    },
    methods: {
        swapText(text) {
            this.button1Text = text
            this.button2Text = this.button1Text === '是的！' ? '不是~' : '是的！'
        },
        swapBack() {
            this.button1Text = '是的！'
            this.button2Text = '不是~'
        },
        handleEnter() {
            this.displayValue = this.inputValue
            this.inputValue = ''
            this.step = 1
        },
        changeThink() {
            let old = 0;
            for (let i = 0; i < this.thinkShow.length; i++){
                if (this.thinkShow[i] === 1) {
                    this.thinkShow[i] = 0
                    old = i
                    break
                }
            }
            let rand = Math.random() * 100 % 4
            while (rand === old) {
                rand = Math.random() * 100 % 4
            }
            rand = Math.floor(rand)
            for (let i = 0; i < this.thinkShow.length; i++) {
                if (i === rand) {
                    this.thinkShow[i] = 1
                    break
                }
            }
        }
    }
}
</script>

<style scoped>
.intro{
    position: fixed;
    left: 50%;
    top: 20%;
    transform: translateX(-50%);
    font-size: 50px;
    color: #FB6D48;
}

.input {
    width: 500px;
    height: 100px;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: #FEC7B4;
    font-size: 64px;
    padding: 15px;
    border: 1px solid #FC819E;
    outline: none;
    background: linear-gradient(to right, #FFF3C7 50%, transparent 50%);
    background-size: 200% 100%;
    background-position: right bottom;
    transition: all 0.5s ease;
}

.input:focus {
    background-position: left bottom;
    box-shadow: 0 0 100px #F7418F;
}

.title{
    position: fixed;
    left: 50%;
    top: 30%;
    transform: translateX(-50%);
    font-size: 50px;
    color: #FB6D48;
}

.btn {
    position: fixed;
    top: 50%;
    width: 20%;
    height: 100px;
    padding: 15px 30px;
    font-size: 30px;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    background-color: #FF8E8F;
    color: #E72929;
}

.confirm{
    left: 25%;
}

.cancel{
    right: 25%;
}

.think{
    position: fixed;
    width: 150px;
    height: 50px;
    font-size: 30px;
    color: #6B76FF;
    background-color: #CEF0B9;
    border: none;
    border-radius: 15px;
}

.think1 {
    top: 10%;
    left: 20%;
}

.think2{
    top: 30%;
    right: 10%;
}

.think3{
    bottom: 30%;
    left: 10%;
}

.think4{
    bottom: 10%;
    right: 40%;
}

.end{
    position: fixed;
    top: 25%;
    left: 50%;
    transform: translateX(-50%);
    font-size: 3rem;
    color: red;
}

.mobile{
    display: none;
}
    
@media only screen and (max-width: 600px){
    .mobile{
        display: block;
        width: 200px;
        height: 100px;
        padding: 30px;
        font-size: 20px;
        text-align: center;
        background-color: white;
        position: fixed;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        border-radius: 20px;
    }
}
</style>
