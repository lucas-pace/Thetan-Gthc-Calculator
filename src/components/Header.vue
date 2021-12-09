<template>
  <header class="navigation">
    <div class="navigation__inner container--large">
      <a href="#" class="logo">
        <span class="sr-only">Thetan Profit Calculator</span>
      </a>
    </div>

  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Header',
  props: {
    lightModeActive: Boolean,
  },
  methods: {
    handleClick() {
      this.$emit('toggle-light-mode');
    },
  },
});
</script>

<style scoped lang="scss">
@use '~styles/1-tools/mixins/tools.media-query' as *;

.navigation {
  grid-area: header;
  padding-top: 3rem;
  padding-bottom: 3rem;
}

.navigation__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo svg {
  width: 100px;
  height: auto;
  fill: var(--color-theme-light);

  @include mq(small) {
    width: 120px;
  }
}

.theme-button {
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-theme-light);
}

.theme-button svg {
  width: 30px;
  height: 30px;
}

.theme-button__moon {
  display: none;
}

.theme-button.is-active .theme-button__moon {
  display: block;
}

.theme-button.is-active .theme-button__sun {
  display: none;
}
</style>
