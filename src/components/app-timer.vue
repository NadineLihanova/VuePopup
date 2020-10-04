<template>
    <transition name="fade">
        <div v-if="show" class="timer">{{currentTime}}</div>
    </transition>
</template>

<script>
export default {
    name: 'Timer',
    data() {
        return {
            currentTime: 3,
            timer: null,
            show: true
        }
    },
    mounted() {
        this.startTimer()
    },
    destroyed() {
        this.stopTimer()
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.currentTime--
            }, 1000)
        },
        stopTimer() {
            clearTimeout(this.timer)
        },
    },
    watch: {
        currentTime(time) {
            if (time === 0) {
                this.stopTimer()
                this.show = false
            }
        }
    }
}
</script>

<style lang="stylus">

.timer
    width 100%
    height 200px
    position absolute
    margin auto 0
    top 0
    bottom 0
    left 0
    right 0
    display flex
    justify-content center
    align-items center
    font-size 200px
    font-weight bold
    color #574b90

.fade-enter-active,
.fade-leave-active 
    transition opacity .5s 

.fade-enter,
.fade-leave-to 
    opacity 0
</style>