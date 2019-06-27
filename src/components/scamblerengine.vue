<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <div id="timer">
            <b-alert show variant="info">
              <span id="minutes">{{ minutes }}</span>
              <span id="middle">:</span>
              <span id="seconds">{{ seconds }}</span>
            </b-alert>
          </div>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <div id="phrase-container">
            <div v-if="isCorrect === true">
              <div id="answer">
                <b-alert show variant="success">Key: "{{ currentPhrase }}"</b-alert>
              </div>
            </div>
            <div v-else-if="isCorrect === false">
              <b-alert show variant="danger">incorrect answer, try again!</b-alert>
            </div>
          </div>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <div id="scrambled-word">
            <b-alert show variant="warning">{{ scrambleCurrentWord }}</b-alert>
          </div>
        </b-col>
      </b-row>
    </b-container>
    <div class="scrambler-container">
      <div class="userinput">
        <b-form-input id="input-1" v-model="input" required placeholder="answer"/>
      </div>
      <div>
        <b-group>
          <b-button v-if="!isStarted" @click="startPuzzle">Start</b-button>
          <b-button v-if="isStarted" @click="checkAnswer" @keydown.enter="checkAnswer">Submit</b-button>
        </b-group>
        <b-button v-if="isCorrect === true" @click="reset">Reset</b-button>
      </div>
    </div>
  </div>
</template>

<script>
import { dictionary } from "../directory/worddictionary";
import { phraseArray } from "../directory/phrase";
import { clearInterval, setInterval } from "timers";

export default {
  name: "scramblerengine",
  data() {
    return {
      // Timer section
      timer: null,
      totalTime: 0.5 * 60,
      // Word section
      currentWord: "",
      isStarted: false,
      currentPhrase: "",
      scrambledCurrentWord: "",
      input: "",
      isCorrect: null,
      dictionary: dictionary,
      phraseArray: phraseArray
    };
  },
  methods: {
    startPuzzle: function() {
      this.isStarted = true;
      this.resetCurrentPhrase();
      this.resetCurrentWord();
      this.startTime();
    },
    startTime: function() {
      this.resetCurrentWord();
      this.resetCurrentPhrase();
      this.timer = setInterval(() => {
        this.countdown();
      }, 1000);
    },
    countdown: function() {
      if (this.totalTime >= 1) {
        this.totalTime--;
      } else {
        this.totalTime = 0;
        this.reset();
      }
    },
    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
    },
    padTime: function(time) {
      return (time < 10 ? "0" : "") + time;
    },
    reset: function() {
      this.totalTime = 0.5 * 60;
      clearInterval(this.timer);
      this.timer = null;
      this.input = "";
      this.currentPhrase = "";
      this.isCorrect = null;
      this.startTime();
    },
    resetCurrentPhrase: function() {
      var randomIndex = Math.floor(Math.random() * this.phraseArray.length);
      this.currentPhrase = this.phraseArray[randomIndex];
    },
    resetCurrentWord: function() {
      var randomIndex = Math.floor(Math.random() * this.dictionary.length);
      this.currentWord = this.dictionary[randomIndex];
    },
    checkAnswer: function() {
      if (this.input.toLowerCase() === this.currentWord) {
        this.stopTimer();
        this.isCorrect = true;
      } else {
        this.input = null;
        this.isCorrect = false;
      }
    }
  },
  created() {
    //this.startTime();
  },
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - this.minutes * 60;
      return this.padTime(seconds);
    },
    scrambleCurrentWord: function() {
      return this.currentWord
        .split("")
        .sort(function() {
          return 0.5 - Math.random();
        })
        .join("");
    }
  }
};
</script>

<style scoped>
#timer {
  font-size: 50px;
  line-height: 1;
}
#phrase-container {
  font-size: 20px;
  line-height: 1;
}
#scrambled-word {
  font-size: 20px;
  font-weight: bold;
  line-height: 1;
}
</style>