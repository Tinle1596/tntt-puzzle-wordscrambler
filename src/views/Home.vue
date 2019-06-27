<template>
  <div class="home">
    <puzzletitle/>
    <scrambler/>
  </div>
</template>

<script>
// @ is an alias to /src
import scrambler from '../components/scamblerengine'
import puzzletitle from '../components/puzzletitle'

export default {
  name: 'home',
  components: {
    scrambler,
    puzzletitle
  }
}
</script>

<style scoped>

</style>
