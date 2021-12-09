<template>
  <footer class="footer">
    <div class="footer__inner container--large">
      <small class="footer__tip">
         Any donate is appreciated <span class="text--ci" aria-hidden="true">♥</span> : 0x315e3a1a07cfeDab70DD6bD980b8d6bEbA67cFDc

      </small>
      <small class="footer__copyright">
        Made by <a href="https://github.com/lucas-pace" target="_blank" rel="noopener noreferrer">Lucas Pace</a>
      </small>
    </div>
  </footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Footer',
});
</script>

<style scoped lang="scss">
@use '~styles/1-tools/mixins/tools.media-query' as *;

.footer {
  padding-top: 2rem;
  padding-bottom: 2rem;
  grid-area: footer;

  @include mq(small) {
    padding-top: 5rem;
    padding-bottom: 5rem;
  }
}

.footer__inner {
  display: flex;
  justify-content: space-between;
}

.footer__tip,
.footer__copyright {
  font-size: 1.5rem;
}
</style>
