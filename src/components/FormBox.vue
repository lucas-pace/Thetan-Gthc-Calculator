<template>
  <div class="frame">
    <div class="frame__inner">
      <div class="grid-container">
        <div class="grid-col grid-col--left">
          <CalculatorSize @calculated="onResultChild"/>
        </div>
        <div class="grid-col grid-col--right text-center">
          <div style="white-space:nowrap">
            <div style="display:inline; white-space:nowrap;">
              {{ this.coins }} gTHC
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CalculatorSize from './CalculatorSize.vue';

export default defineComponent({
  name: 'FormBox',
  data() {
    return {
      coins: '0',
    };
  },
  components: {
    CalculatorSize,
  },
  methods: {
    onResultChild(value : any) {
      this.coins = (Math.round(value * 100) / 100).toFixed(2);
    },
  },
});
</script>

<style scoped lang="scss">
@use '~styles/1-tools/mixins/tools.media-query' as *;

.grid-container {
  position: relative;
  z-index: 1;
  display: block;

  @include mq(small) {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 5rem;
  }

  @include mq(large) {
    gap: 10rem;
  }
}

.grid-col--right {
  margin-top: 5rem;

  @include mq(small) {
    margin-top: 0;
  }
}
</style>
