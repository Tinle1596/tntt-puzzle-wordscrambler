<template>
  <div id="header">
    <b-alert show variant="info">
      <h4>Tntt word scrambler</h4>
      <div>Instructions:</div>
      <b-container>
        <b-row>
          <b-col id="instruction-details">
            <p>Solve the scrambled word before timer runs out.</p>
            <p>One correct answer will give you a random key phrase, there are six in total.</p>
            <p>Organize the phrases into the correct sentence and show Huynh Truong.</p>
          </b-col>
        </b-row>
      </b-container>            
    </b-alert>
  </div>
</template>

<script>
export default {

};
</script>

<style scoped>
#instruction-details{
  font-size: 12px;
  font-weight: bold;
}
p{
  margin: 0;
  padding: 0;
}
</style>