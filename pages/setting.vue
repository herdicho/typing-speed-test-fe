<template>
  <div>
    <SaveCompletedModal :isVisible="modalVisible" @cancel="modalVisible = false"/>
    <!-- <ScoreModal :isVisible="modalVisible" :score="50" @cancel="modalVisible = false"/> -->
    <NavBarModal />
    <div class="container mx-auto border-4 border-blue-500 h-auto rounded-lg mt-16 w-3/5">
      <div class="flex">
        <div class="border-r-4 border-blue-500 w-2/6">  
          <div class="text-blue-500 text-mono m-8 text-5xl"> <span class="font-bold">Hello,</span> Dummy</div>       
          <div v-if="isTimeActive" class="cursor-pointer border-t-4 text-white bg-blue-500 border-b-2 text-3xl font-bold border-blue-500">
            <div @click="getCurrentTimeSetting()" class="m-4">
              TIME
            </div>  
          </div>       
          <div v-else @click="isTimeActive=true, isWordLanguageActive=false" class="cursor-pointer border-t-4 text-blue-500 border-b-2 text-3xl font-bold border-blue-500">
            <div @click="getCurrentTimeSetting()" class="m-4">
              TIME
            </div>  
          </div>  
          <div v-if="isWordLanguageActive" class="cursor-pointer border-t-2 text-white bg-blue-500 border-b-2 text-3xl font-bold border-blue-500">
            <div class="m-4">
              WORD LANGUAGE
            </div>  
          </div> 
          <div v-else @click="isTimeActive=false, isWordLanguageActive=true" class="cursor-pointer border-t-2 text-blue-500 text-3xl font-bold border-blue-500">
            <div class="m-4">
              WORD LANGUAGE
            </div>  
          </div>         
        </div>
        <div class="w-4/6"> 
          <div v-if="isTimeActive" class="h-full">
            <div class="flex justify-between mx-auto h-1/2">
              <button v-if="isThirtySecondActive" class="m-auto w-32 bg-blue-500 font-bold text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                30 DETIK
              </button>
              <button v-else @click="changeCurrentTimeSetting('30s')" class="m-auto w-32 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                30 DETIK
              </button>
              <button v-if="isOneMinuteActive" class="m-auto w-32 bg-blue-500 font-bold text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                1 MENIT
              </button>
              <button v-else @click="changeCurrentTimeSetting('1m')" class="m-auto w-32 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                1 MENIT
              </button>
              <button v-if="isTwoMinuteActive" class="m-auto w-32 bg-blue-500 font-bold text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                2 MENIT
              </button>
              <button v-else @click="changeCurrentTimeSetting('2m')" class="m-auto w-32 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                2 MENIT
              </button>
            </div>
            <div class="flex justify-center mx-auto h-1/2">
              <button @click="getCurrentTimeSetting()" class="mx-auto w-36 h-16 mt-6 bg-transparent hover:bg-red-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                CANCEL
              </button>
              <button @click="setCurrentTimeSetting()" class="mx-auto w-36 h-16 mt-6 bg-transparent hover:bg-green-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                SAVE
              </button>
            </div>
          </div>   
          <div v-else class="h-full">
            <!-- <div class="flex justify-between mx-auto h-1/2">
              <button v-if="isThirtySecondActive" class="m-auto w-32 bg-blue-500 font-bold text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                INDONESIA
              </button>
              <button v-else @click="changeCurrentTimeSetting('30s')" class="m-auto w-32 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                INDONESIA
              </button>
              <button v-if="isOneMinuteActive" class="m-auto w-32 bg-blue-500 font-bold text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                ENGLISH
              </button>
              <button v-else @click="changeCurrentTimeSetting('1m')" class="m-auto w-32 bg-transparent hover:bg-blue-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                ENGLISH
              </button>
            </div>
            <div class="flex justify-center mx-auto h-1/2">
              <button @click="getLanguageSetting()" class="mx-auto w-36 h-16 mt-6 bg-transparent hover:bg-red-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                CANCEL
              </button>
              <button @click="setLanguageSetting()" class="mx-auto w-36 h-16 mt-6 bg-transparent hover:bg-green-500 text-blue-500 font-bold hover:text-white py-4 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
                SAVE
              </button>
            </div> -->
          </div>   
        </div>
      </div>  
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import NavBarModal from '~/components/NavBarModal.vue';
import SaveCompletedModal from '~/components/SaveCompletedModal.vue';
import ScoreModal from '~/components/ScoreModal.vue';
@Component({
    components: {
      NavBarModal,
      SaveCompletedModal,
      ScoreModal,
    }
  })
export default class Setting extends Vue {
  
  isTimeActive : boolean = false
  isWordLanguageActive : boolean = false
  isThirtySecondActive : boolean = false
  isOneMinuteActive : boolean = false
  isTwoMinuteActive : boolean = false
  modalVisible : boolean = false

  set30SecondTimeToActive() : void {
    this.isThirtySecondActive = true
    this.isOneMinuteActive = false
    this.isTwoMinuteActive = false
  }

  set1MinuteTimeToActive() : void {
    this.isThirtySecondActive = false
    this.isOneMinuteActive = true
    this.isTwoMinuteActive = false
  }

  set2MinuteTimeToActive() : void {
    this.isThirtySecondActive = false
    this.isOneMinuteActive = false
    this.isTwoMinuteActive = true
  }

  getCurrentTimeSetting() : void {
    const curTimeSetting : string | null = localStorage.getItem("currentTimeSetting")

    if (curTimeSetting === null) {
      this.set30SecondTimeToActive()
    } else {
      if (curTimeSetting === "1m") {
        this.set1MinuteTimeToActive()
      } else if (curTimeSetting === "2m") {
        this.set2MinuteTimeToActive()
      } else {
        this.set30SecondTimeToActive()
      } 
    }
  }

  changeCurrentTimeSetting(time : string) : void {
    if (time === "30s") {
      this.set30SecondTimeToActive()
    } else if (time === "1m") {
      this.set1MinuteTimeToActive()
    } else if (time === "2m") {
      this.set2MinuteTimeToActive()
    }
  }

  setCurrentTimeSetting() : void {
    if (this.isThirtySecondActive) {
      localStorage.setItem("currentTimeSetting", "30s")
    } else if (this.isOneMinuteActive) {
      localStorage.setItem("currentTimeSetting", "1m")
    } else if (this.isTwoMinuteActive) {
      localStorage.setItem("currentTimeSetting", "2m")
    }

    this.modalVisible = true
  }

  mounted() {
    this.isTimeActive = true
    this.isWordLanguageActive = false
    this.getCurrentTimeSetting()
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

  .current-active {
    background-color: lightblue;
  }

</style>
