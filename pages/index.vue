<template>
  <div class="container md mx-auto">

        <div class="grid grid-cols-1 pt-24">
            <h1 class="m-auto text-5xl font-mono"><strong> SPEED TYPING TEST </strong></h1>
        </div> 
    
        <div class="grid grid-cols-1 pt-6 w-3/4 mx-auto">
            <div class="grid justify-items-center h-20 bg-transparent border-2 border-black px-3 min-w-3/4 min-h-3/4"> 
                <div class="text-display m-auto text-md text-2xl text-gray-600 font-mono" id="textDisplay">  </div>
            </div>
        </div>
    
        <div class="grid grid-cols-2 pt-6 w-2/6 mx-auto">
            <div class="grid justify-items-center h-20"> 
                <input v-on:keyup="checkAnswer($event)" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline font-mono" id="inputText" type="text" placeholder="Type to Start ....">
            </div>   

            <div class="grid justify-items-center h-20"> 
              <button @click="startGame()" class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded text-mono">
                Click to start !!!
              </button>
            </div>
    
            <div class="grid justify-items-center h-20"> 
                <div class="font-mono timer m-auto text-5xl" id="timer"> {{timer}} </div>
            </div>

            <div class="grid justify-items-center h-20"> 
                <div class="font-mono score m-auto text-5xl" id="score"> 0 </div>
            </div>
        </div>
        
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
@Component
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
  ]

  scoreElement : any = ""
  quoteDisplayElement : any = ""
  quoteInputElement : any = ""

  timer : number = 0  
  word_span : string = ""
  word_question : string = ""
  word_answer : string = ""

  score : number = 0 
  global_index : number = 0

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

  checkAnswer(event:any) {
    const arrayQuote = this.quoteDisplayElement.querySelectorAll('span')[this.global_index]
    const arrayValue = this.quoteInputElement.value
    arrayQuote.classList.add('current-text')

    const word_question = arrayQuote.innerText
    const word_answer = arrayValue
    const word_span = arrayQuote

    if (event.code === 'Space') {
      let is_correct = true
      const splitArrayQuote = word_question.split('')
      const splitArrayValue = word_answer.replace(/\s*$/,'').split('')
      splitArrayValue.forEach((char:any,index:any) => {
        if (char != splitArrayQuote[index]) {
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
        this.scoreElement.innerText = this.score
        this.checkIsAllQuestionCorrect()
      } else {
        word_span.classList.remove('correct')
        word_span.classList.add('incorrect')
      }
    }
  }

  outputWord() {
    this.quoteDisplayElement.innerHTML = ''
    this.words.forEach(word => {
      const wordSpan = document.createElement('span')
      wordSpan.innerText = word 
      wordSpan.classList.add('mr-2')
      this.quoteDisplayElement.appendChild(wordSpan)
    })
    this.quoteInputElement.value = ''
  }

  startTimer() {
    let time = 5

    const timer = setInterval(() => {
      this.timer = time
      console.log(time)
      time -= 1
      if (time == -1) {
        const message = "score : " + this.score
        alert(message)
        clearInterval(timer)
        this.resetGame()
      } 
    }, 1000)
  }

  resetGame() {
    this.scoreElement.innerText = 0
    this.quoteInputElement.value = ''
    this.quoteDisplayElement.innerHTML = ''
    this.score = 0
    this.global_index = 0
    this.quoteInputElement.disabled = true
  }

  startGame() {
    this.startTimer()
    this.outputWord()
    this.quoteInputElement.disabled = false
    this.quoteInputElement.focus()
  }

  mounted() {
    this.scoreElement = document.getElementById('score')
    this.quoteDisplayElement = document.getElementById('textDisplay')
    this.quoteInputElement = document.getElementById('inputText')
    this.quoteInputElement.disabled = true
  }
}
</script>

<style>
    * {
        box-sizing: border-box;
    }
  
    body {
      background-color: blanchedalmond;
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
      padding: 5px;
    }
</style>
