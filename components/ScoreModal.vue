<template>
    <div v-if="isVisible">
    <div class="fixed inset-0 z-50 flex justify-center items-center">
        <div class="flex flex-col max-w-5xl rounded-lg shadow-lg bg-yellow-100">
            <div class="p-5">
                <div class="flex justify-between items-start">
                    <h3 class="m-auto text-8xl font-mono p-5">GAME OVER</h3>
                </div>
            </div>

            <div class="text-4xl font-mono font-bold p-6">
                <p>Your Score : {{score}}</p>
            </div>

            <div class="p-6 flex justify-end items-center">
                <button @click="emitCancel" class="bg-transparent hover:bg-black text-2xl font-mono font-bold btn-outline hover:text-white py-2 px-4 border border-black hover:border-transparent rounded">
                    CLOSE
                </button>
            </div>

            
        </div>
    </div>
    <div class="opacity-25 fixed inset-0 z-40 bg-black"></div>
</div>
</template>

<script lang='ts'>
  import Component from 'vue-class-component';
  import Vue from 'vue';
  import { Prop } from 'vue-property-decorator';
  @Component({})
  export default class ScoreModal extends Vue {
    @Prop() isVisible!: boolean;
    @Prop() score!: number;

    emitCancel() {
      this.$emit('cancel');
    }
  }
</script>