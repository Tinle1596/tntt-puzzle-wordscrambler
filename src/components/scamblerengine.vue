<template>
  <div>
      <div>
        The name of our doan is: {{ scrambleInput1 }}
    </div>
    <div>
      <b-form-input id="input-1" v-model="input1" required placeholder="answer"/>
    </div>
    <div>
      <b-button @click="checkAnswer('EMMANUEL')">Submit</b-button>
    </div>
  </div>
</template>

<script>
import { dictionaryV1, dictionaryV2 } from "../directory/alphabetdictionary";
import { phrasePart1, phrasePart2 } from "../directory/phrase";

export default {
  name: "scramblerengine",
  data() {
    return {
      input1: '',
      input2: '',
      scramInput1: '',
      dictionaryV1: dictionaryV1,
      dictionaryV2: dictionaryV2,
      phrasePart1: phrasePart2,
      phrasePart2: phrasePart2,
      
    };
  },
  computed: {
      scrambleInput1: function(){
          var dictionary = this.dictionaryV1;
          var scrambledInput1 = '';
          var input1 = this.input1.toUpperCase().trim().split(''); //split into array
          input1.forEach(function(letter){
              var scrambledLetter = dictionary[letter]
              scrambledInput1 += scrambledLetter
              console.log(scrambledInput1)
          });
          this.scramInput1 = scrambledInput1;
          return scrambledInput1;
      }      
  },
  methods: {
      checkAnswer: function(input) {
         var userInput = this.scramInput1
          if(userInput === input){
              console.log('right answer!')
          }else{
              console.log('incorrect answer!')
          }
      }
  }
};
</script>

<style lang="scss" scoped>
</style>