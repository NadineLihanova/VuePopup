<template>
    <div class="container">
        <transition name="fade">
            <div class="overlay" v-if="show" @click="hidePopup()"></div>
        </transition>
        <transition name="slide">
            <div class="popup" v-if="show">
                <div class="popup__close" @click="hidePopup()">
                    <svg width="24" height="24" fill="#ffffff" xmlns="http://www.w3.org/2000/svg">
                        <path d="M7.06069 5.64645C6.86543 5.45118 6.54884 5.45118 6.35358 5.64645L5.64648 6.35355C5.45121 6.54882 5.45121 6.8654 5.64648 7.06066L10.5858 12L5.64645 16.9393C5.45118 17.1346 5.45118 17.4512 5.64645 17.6464L6.35355 18.3536C6.54882 18.5488 6.8654 18.5488 7.06066 18.3536L12 13.4142L16.9393 18.3536C17.1346 18.5488 17.4512 18.5488 17.6464 18.3536L18.3536 17.6464C18.5488 17.4512 18.5488 17.1346 18.3536 16.9393L13.4142 12L18.3536 7.06066C18.5488 6.8654 18.5488 6.54882 18.3536 6.35355L17.6465 5.64645C17.4512 5.45118 17.1346 5.45118 16.9394 5.64645L12 10.5858L7.06069 5.64645Z" />
                    </svg>
                </div>
                <div class="popup__body">
                    <slot></slot>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
export default {
    name: 'AppPopup',
    data() {
        return {
            show: false
        }
    },
    created() {
        setTimeout(this.showPopup, 3000);
    },
    methods: {
        showPopup() {
            this.show = true;
            document.body.classList.add('stop-scroll');
        },
        hidePopup() {
            this.show = false;
            document.body.classList.remove('stop-scroll');
        }
    }
}
</script>

<style lang="stylus">

.container
    width 100%
    min-height 100vh
    position relative
    display flex
    justify-content center
    align-items center
    overflow-x hidden

.overlay
    position absolute
    top 0
    bottom 0
    left 0
    right 0
    z-index 8   
    background-color rgba(120, 111, 166, .9)

.popup
    width 95%
    max-width 550px
    height 40vh
    min-height 400px
    padding 50px
    display flex
    position relative
    top -100vh
    transform translateY(100vh)
    background none
    box-sizing border-box
    z-index 9
    &__close
        width 40px
        height 40px
        padding 6px
        position absolute
        top 0
        right 0
        border-radius 50%
        border 2px solid #fff
        box-sizing border-box
        cursor pointer
        transition transform .5s
        &:hover
            transform rotate(180deg)
    &__body 
        width 100%
        padding 30px
        background #ffffff
        border-radius 20px
        box-shadow 0 15px 10px rgba(0,0,0,0.2)
        box-sizing border-box

.fade-enter-active,
.fade-leave-active 
    transition opacity 2s 


.fade-enter,
.fade-leave-to 
    opacity 0

.slide-enter-active,
.slide-leave-active {
    transition transform 2s ease-out
}

.slide-enter,
.slide-leave-to 
    transform translateY(-100vh)


</style>