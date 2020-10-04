<template>
    <div>
        <app-timer></app-timer>
        <app-popup>
          <app-form></app-form>
        </app-popup>
    </div>
</template>

<script>
import AppPopup from '../components/app-popup'
import AppForm from '../components/app-form'
import AppTimer from '../components/app-timer'

export default {
  name: 'Home',
  components: {
    AppPopup,
    AppForm,
    AppTimer
  }
}
</script>

<style lang="stylus">

</style>
