<template>
    <div class="form">
        <transition name="fade">
            <div 
                v-if="sended"
                class="form__message"
            >
                Спасибо!
            </div>
        </transition>
        <div
            v-if="!sended" 
            class="form__body"
        >
            <div class="form__item">
                <input 
                    v-model.trim="email" 
                    @blur="$v.email.$touch()"
                    type="text" 
                    id="email" 
                    class="form__input" 
                    :class="{'form__input_error' : $v.email.$error }"
                    placeholder="Введите email"
                >
                <transition name="fade">
                    <div 
                        v-if="$v.email.$error"
                        class="form__error"
                    >
                        <span v-if="!$v.email.email">
                            Неверный email
                        </span>
                        <span v-else>
                            Заполните поле
                        </span>
                    </div>
                </transition>
            </div>
            <div 
                class="form__button"
                :class="{'form__button_disable' : $v.email.$error }"
                @click="submit()"
            >
                Поехали!
            </div>
        </div>
    </div>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators'

export default {
    name: 'AppForm',
    data() {
        return {
            email: '',
            sended: false
        }
    },
    validations: {
        email: {
            required,
            email
        }
    },
    methods: {
        async send() {
            let promise = new Promise((resolve) => {
                setTimeout(() => resolve('success'), 2000)
            });
            let result = await promise;
            if (result === 'success') {
                console.log('email: ', this.email);
            }
        },
        submit() {
            this.$v.email.$touch();
            if (!this.$v.email.$error) {
                this.sended = true;
                this.send();               
            }
        }
    }
}
</script>

<style lang="stylus">

.form
    width 100%
    height 100%
    display flex
    flex-direction column
    &__message
        display flex
        justify-content center
        align-items center
        flex-grow 1
        color #303952
        font-size 40px
        font-weight bold
    &__body
        width 100%
        text-align center
    &__item
        position relative
    &__input
        display flex
        width 100%
        margin 30px 0
        padding 15px
        border 2px solid #574b90
        border-radius 5px
        font-size 16px
        color #303952
        box-sizing border-box
        &::placeholder
            color #574b90
        &:focus
            outline none
        &_error
          border 2px solid #c44569
    &__error
        position absolute
        margin 0 auto
        left 0
        right 0
        top 75px
        color #c44569
    &__button
        display inline-block
        padding 15px 30px
        margin 35px 0 0 0
        color #ffffff
        font-size 20px
        background #574b90
        border-radius 5px
        box-shadow 0 5px 10px rgba(0,0,0,0.2)
        transition-property background
        transition-duration .5s
        cursor pointer
        &:hover
            background #303952
        &_disable
            background #786fa6
            cursor default
            &:hover
                background #786fa6

.fade-enter-active,
.fade-leave-active 
    transition opacity .5s 

.fade-enter,
.fade-leave-to 
    opacity 0

</style>