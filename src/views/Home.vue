<template>
  <div class="home">
    <div>this is the header</div>
    <scrambler/>
  </div>
</template>

<script>
// @ is an alias to /src
import scrambler from '../components/scamblerengine'

export default {
  name: 'home',
  components: {
    scrambler
  }
}
</script>
