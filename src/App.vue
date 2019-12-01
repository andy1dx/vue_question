<template>
  <div id="app">
    <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <div class="bv-example-row container">
      <div class="row">
        <div class="col-sm-6 offset-3">
         <QuestionsBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
         />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionsBox from './components/QuestionsBox.vue'

export default {
  name: 'app',
  components: {
    Header,
    QuestionsBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
   next() {
     this.index++;
   },
   increment(isCorrect) {
     if(isCorrect) {
      this.numCorrect++
     }
     this.numTotal++
   }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=15&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((json_data) => {
       this.questions = json_data.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
