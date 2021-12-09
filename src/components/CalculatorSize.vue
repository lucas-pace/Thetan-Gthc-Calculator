<template>
  <form class="form" @submit.prevent="calculategTHC">
    <!-- <legend class="form__legend">Calculate image size</legend> -->

    <div class="form__wrapper">
      <div class="form__item">
        <label class="form__label" for="calc-winrate">
          Win Rate ( value between 0 and 1 )<span class="mandatory">*</span>
        </label>
        <input
          class="form__input"
          id="calc-winrate"
          v-model="winrate"
          placeholder="For 50% winrate use 0.5"
          :aria-invalid="winrateHasError"
          aria-describedby="winrate-size-error"
          autocomplete="off"
        >
        <span id="winrate-size-error" class="form__error" v-show="winrateHasError">Only numbers and "." are allowed!</span>
      </div>

      <div class="form__item">
        <label class="form__label" for="calc-battles">Remaining Battles ( max gTHC battles of hero - Battle already played )</label>
        <input
          class="form__input"
          id="calc-battles"
          v-model="battles"
          :aria-invalid="rarityHasError"
          aria-describedby="battles-size-error"
          autocomplete="off"
        >
        <span id="battles-size-error" class="form__error" v-show="battlesHasError">Only numbers are allowed!</span>
      </div>

     <div class="form__item">

       <label class="form__label" for="calc-rarity">Hero Rarity</label><br>
         <select name="rarity_id" @change="onChange($event)" v-model="key" class="form-select form-control">
            <option value="-1">---- Select Hero Rarity ----</option>
            <option value="common">Common</option>
            <option value="epic">Epic</option>
            <option value="legendary">Legendary</option>
         </select>
      </div>

      <div class="form__item form__item--submit">
        <button class="button" @click="calculategTHC">Calculate gTHC</button>
        <button class="button--round" @click="resetForm">
          <span class="button__icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 768 768" aria-hidden="true">
              <path fill="currentColor" d="M384 0c-103.241 0-199.79 42.624-270.611 113.389l-113.389-113.389v329.143h329.143l-138.404-138.404c50.578-50.579 119.534-81.024 193.262-81.024 151.241 0 274.285 123.044 274.285 274.285s-123.044 274.285-274.286 274.285c-73.234 0-142.080-28.58-193.92-80.365l-77.568 77.568c72.521 72.521 168.96 112.512 271.488 112.512 211.693 0 384-172.306 384-384 0-211.748-172.306-384-384-384z"/>
            </svg>
          </span>
          <span class="sr-only">Reset Form</span>
        </button>
      </div>
    </div>
  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { inputTypes } from '../types';

export default defineComponent({
  name: 'CalculatorSize',
  data() {
    return {
      battles: '',
      rarity: '',
      key: '-1',
      winrate: '',
      battlesHasError: false,
      rarityHasError: false,
      winrateHasError: false,
      lastInputUsed: '' as inputTypes,
    };
  },
  methods: {
    calculategTHC() {
      let result = 0;
      const floatWinrate = parseFloat(this.winrate);
      const floatBattles = parseFloat(this.battles);
      let winCoin = 0;

      if (parseFloat(this.winrate) > 1 || parseFloat(this.winrate) < 0) return;

      if (!this.winrate || (!this.rarity && !this.battles)) return;

      if (this.battles && this.rarity) {
        switch (this.rarity) {
          case 'common': winCoin = 3.25 + 6;
            break;
          case 'epic': winCoin = 6.5 + 6;
            break;
          case 'legendary': winCoin = 23.55 + 6;
            break;
          default: break;
        }

        const moedasGanhasWin = floatWinrate * floatBattles * winCoin;
        const moedasGanhasLose = (1 - floatWinrate) * floatBattles;
        result = moedasGanhasWin + moedasGanhasLose;
        const batalhasPorDia = 10;
        const dias = floatBattles / batalhasPorDia;
        this.$emit('calculated', result);
      }
    },
    resetForm() {
      this.$emit('calculated', 0);
      this.key = '-1';
      this.battles = '';
      this.rarity = '';
      this.winrate = '';
      this.battlesHasError = false;
      this.rarityHasError = false;
      this.winrateHasError = false;
    },
    onChange(e : any) {
      this.rarity = e.target.value;
    },
  },

});

</script>

<style scoped lang="scss">
</style>
