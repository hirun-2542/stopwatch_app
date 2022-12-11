<script setup>
import { ref } from "vue";

const min = ref(0);
const sec = ref(0);
const msec = ref(0);
const Interval = ref();

const displayTime = () => {
    msec.value++;
    if (msec.value === 100) {
        msec.value = 0;
        sec.value++;
    }
    if (sec.value === 60) {
        sec.value = 0;
        min.value++;
    }
};

const start = () => {
  clearInterval(Interval.value);
  Interval.value = setInterval(displayTime, 10);
};

const reset = () => {
    clearInterval(Interval.value);
    min.value = 0;
    sec.value = 0;
    msec.value = 0;
};

const stop = () => {
    clearInterval(Interval.value);
};
</script>

<template>
    <div class="watch-app">
        <div class="watch">
            <div class="watch__time">
                <span class="watch__time--min">{{ (min < 10) ? '0' + min.toString() : min.toString() }} : </span>
                <span class="watch__time--sec">{{ (sec < 10) ? '0' + sec.toString() : sec.toString() }} : </span>
                <span class="watch__time--msec">{{ (msec < 10) ? '0' + msec.toString() : msec.toString() }} </span>
            </div>
            <div class="watch__btn">
                <button class="watch__btn--start" @click="start">Start</button>
                <button class="watch__btn--stop" @click="stop">Stop</button>
                <button class="watch__btn--reset" @click="reset">Reset</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.watch-app {
    height: 100vh;
    background-color: #448aff;
}

.watch {
    background-color: #ffffff;
    width: 40%;
    min-width: 500px;
    position: absolute;
    transform: translate(-50%,-50%);
    top: 50%;
    left: 50%;
    padding: 20px 0;
    padding-bottom: 50px;
    border-radius: 10px;
}
.watch__time {
    position: relative;
    width: 92%;
    left: 4%;
    padding: 40px 0;
    font-family: 'Roboto mono',monospace;
    color: #0381bb;
    font-size: 40px;
    display: flex;
    align-items: center;
    justify-content: space-around;
    border-radius: 5px;
    box-shadow: 0 0 20px rgba(0,139,253,0.25);
}

.watch__btn{
    width: 90%;
    margin: 60px auto 0 auto;
    display: flex;
    justify-content: space-around;
}
.watch__btn button{
    width: 120px;
    height: 45px;
    background-color:#20b380;
    color: #ffffff;
    border: none;
    font-family: 'Poppins',sans-serif;
    font-size: 18px;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
}
.watch__btn button:hover{
    background-color: #11e198;
}
.watch__btn button:nth-last-child(2){
    background-color: #d23332;
}
.watch__btn button:nth-last-child(2):hover{
    background-color: #e80a0a;
}
.watch__btn button:nth-last-child(1){
    background-color:  #205e94;
}
.watch__btn button:nth-last-child(1):hover{
    background-color:  #1770bf;
}
</style>
