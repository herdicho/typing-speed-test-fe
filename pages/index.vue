<template>
  <div class="container mx-auto">
        <ScoreModal :isVisible="modalVisible" :score="user_score" @cancel="modalVisible = false"/>
        <NavBarModal />
                 
        <div class="grid grid-cols-1 pt-10">
            <h1 class="m-auto text-5xl font-mono mb-6 text-blue-500"><strong> SPEED TYPING TEST </strong></h1>
        </div> 

        <div class="grid grid-cols-3 pt-20">
          <div class="h-auto w-auto mx-auto text-5xl font-bold text-blue-500" id="score">
            SCORE : 0
          </div>
          <div class="h-auto w-auto mx-auto text-5xl font-bold text-blue-500">
            TIMER : {{timer}}
          </div>
          <div class="border h-auto w-auto border-black mx-auto">
          </div>
        </div>
    
        <div class="grid grid-cols-1 pt-6 w-3/4 mx-auto h-20 mb-20 mt-10">
            <div class="grid justify-items-center bg-transparent border-4 border-blue-500 px-3 min-w-3/4"> 
                <div class="text-display m-auto text-md text-2xl text-gray-600 font-mono" id="textDisplay">  HOW FAST ARE YOU ?? </div>
            </div>
        </div>

        <div class="flex flex-row justify-center items-center">
          <div class="mx-8"> 
                <input v-on:keyup="checkAnswer($event)" class="h-24 w-1/2 bg-transparent shadow appearance-none border-4 border-blue-500 rounded py-2 px-3 text-gray-700 text-4xl text-center leading-tight focus:outline-none focus:shadow-outline font-mono my-2" id="inputText" type="text">
            </div>   

            <div class="mx-8"> 
              <button @click="startGame()" class="h-20 w-30 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-2 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono" id="startButton">
                CLICK TO START !!!
              </button>
            </div>
        </div>
        
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import ScoreModal from '~/components/ScoreModal.vue';
import NavBarModal from '~/components/NavBarModal.vue';
@Component({
    components: {
      ScoreModal,
      NavBarModal,
    }
  })
export default class Index extends Vue {

  words : Array<string> = [
    'karena',
    'tidak',
    'bentuk',
    'dapat',
    'jawaban',
    'binatang',
    'tumbuhan',
    'bunga',
    'makan',
    'minum',
    'baca',
    'tulis'
  ]

  scoreElement : any = ""
  quoteDisplayElement : any = ""
  quoteInputElement : any = ""
  startButtonElement : any = ""

  time : number = 50
  timer : number = 0  
  word_span : string = ""
  word_question : string = ""
  word_answer : string = ""

  score : number = 0 
  user_score : number = 0
  global_index : number = 0
  modalVisible : boolean = false

  isLoggedIn : boolean = false

  checkIsAllQuestionCorrect() {
    const arrayQuote = this.quoteDisplayElement.querySelectorAll('span')
    let is_all_correct = true
    arrayQuote.forEach((quote:any) => {
      if (!quote.classList.value.includes('correct')) {
        is_all_correct = false
      }
    })

    if (is_all_correct) {
      this.global_index = 0
      this.outputWord()
    }
  }

  checkAnswer(e : any) {
    const arrayQuote = this.quoteDisplayElement.querySelectorAll('span')[this.global_index]
    const arrayValue = this.quoteInputElement.value
    arrayQuote.classList.add('current-text')

    const word_question = arrayQuote.innerText
    const word_answer = arrayValue
    const word_span = arrayQuote

    if (e.keyCode === 32) {
      this.quoteInputElement.value = this.quoteInputElement.value.slice(0, -1)
    }

    if (word_answer.length === word_question.length) {
      let is_correct = true
      const splitArrayQuote = word_question.split('')
      const splitArrayValue = word_answer.replace(/\s*$/,'').split('')
      splitArrayQuote.forEach((char:any,index:any) => {
        if (char != splitArrayValue[index]) {
          is_correct = false
        }
      })

      if (is_correct) {
        word_span.classList.remove('incorrect')
        word_span.classList.add('correct')
        this.global_index ++
        this.quoteInputElement.value = ''
        word_span.classList.remove('current-text')
        this.score++
        this.scoreElement.innerText = `SCORE : ${this.score}`
        this.checkIsAllQuestionCorrect()
      } else {
        word_span.classList.remove('correct')
        word_span.classList.add('incorrect')
        this.quoteInputElement.value = ''
      }
    }
  }

  outputWord() {
    this.quoteDisplayElement.innerHTML = ''
    for (let i = 0; i < this.words.length; i++) {
      const word = this.words[Math.floor(Math.random() * this.words.length)];
      const wordSpan = document.createElement('span')
      wordSpan.innerText = word 
      wordSpan.classList.add('m-2')
      wordSpan.classList.add('inline-block')
      this.quoteDisplayElement.appendChild(wordSpan)
    }
    this.quoteInputElement.value = ''
  }

  startTimer() {
    this.timer = this.time
    const timer = setInterval(() => {
      this.time -= 1
      this.timer = this.time
      if (this.time == 0) {
        this.user_score = this.score
        clearInterval(timer)
        this.resetGame()
        this.modalVisible = true
      } 
    }, 1000)
  }

  resetGame() {
    this.timer = 0
    this.time = 50
    this.score = 0
    this.scoreElement.innerText = "SCORE : " + this.score
    this.quoteInputElement.value = ''
    this.quoteDisplayElement.innerHTML = ''
    this.global_index = 0
    this.quoteInputElement.disabled = true
    this.startButtonElement.disabled = false
  }

  startGame() {
    this.startTimer()
    this.outputWord()
    this.quoteInputElement.disabled = false
    this.quoteInputElement.focus()
    this.startButtonElement.disabled = true
  }

  mounted() {
    this.scoreElement = document.getElementById('score')
    this.quoteDisplayElement = document.getElementById('textDisplay')
    this.quoteInputElement = document.getElementById('inputText')
    this.startButtonElement = document.getElementById('startButton')
    this.quoteInputElement.disabled = true
  }
}
</script>

<style>
    * {
        box-sizing: border-box;
    }
  
    body {
      background-color: rgb(205, 237, 255);
    }

    .correct {
      color: green;
    }
    
    .incorrect {
      color: red;
      text-decoration: underline;
    }

    .current-text {
      background-color: lightblue;
    }
</style>
