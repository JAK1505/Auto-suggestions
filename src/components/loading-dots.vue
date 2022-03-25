<template>
  <svg
    height="17px"
    width="75px"
  >
    <g transform="translate(15, 8)">
      <circle
        :class="['loading-dot', 'loading-dot-1',
                 {['loading-dots-white']: fillWhite }]"
        :r="radius"
      />
    </g>
    <g transform="translate(39, 8)">
      <circle
        :class="['loading-dot', 'loading-dot-2',
                 {['loading-dots-white']: fillWhite }]"
        :r="radius"
      />
    </g>
    <g transform="translate(63, 8)">
      <circle
        :class="['loading-dot', 'loading-dot-3',
                 {['loading-dots-white']: fillWhite }]"
        :r="radius"
      />
    </g>
  </svg>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    fillWhite: {
      type: Boolean,
      default: false,
    },
    radius: {
      type: Number,
      default: 4,
    },
  },
});
</script>

<style>
  @keyframes pulse-1 {
    0% {
      transform: scale(1, 1);
    }
    25% {
      transform: scale(2, 2);
    }
    50% {
      transform: scale(1.5, 1.5);
    }
    75% {
      transform: scale(1, 1);
    }
    100% {
      transform: scale(1, 1);
    }
  }
  @keyframes pulse-2 {
    0% {
      transform: scale(1, 1);
    }
    25% {
      transform: scale(1, 1);
    }
    50% {
      transform: scale(2, 2);
    }
    75% {
      transform: scale(1.5, 1.5);
    }
    100% {
      transform: scale(1, 1);
    }
  }
  @keyframes pulse-3 {
    0% {
      transform: scale(1, 1);
    }
    25% {
      transform: scale(1, 1);
    }
    50% {
      transform: scale(1, 1);
    }
    75% {
      transform: scale(2, 2);
    }
    100% {
      transform: scale(1.5, 1.5);
    }
  }
  .loading-dot {
    animation-duration: 1s;
    animation-iteration-count: infinite;
    fill: #3498DB;
  }

  .loading-dot-1 {
    animation-name: pulse-1;
  }
  .loading-dot-1 {
    animation-name: pulse-2;
  }
  .loading-dot-1 {
    animation-name: pulse-3;
  }
  .loading-dots-white {
    fill: white;
  }
</style>
