<template>
  <div
    class="c-easingEdit u-position-cover"
    @touchmove="move"
    @touchend.prevent="up"
  >
    <svg
      class="c-easingEdit-lines u-position-cover"
      viewBox="0 0 1 1"
    >
      <line
        class="c-easingEdit-thinLine"
        x1=".25"
        y1="0"
        x2=".25"
        y2="1"
      />
      <line
        class="c-easingEdit-thinLine"
        x1=".5"
        y1="0"
        x2=".5"
        y2="1"
      />
      <line
        class="c-easingEdit-thinLine"
        x1=".75"
        y1="0"
        x2=".75"
        y2="1"
      />
      <line
        class="c-easingEdit-thinLine"
        x1="0"
        y1=".25"
        x2="1"
        y2=".25"
      />
      <line
        class="c-easingEdit-thinLine"
        x1="0"
        y1=".5"
        x2="1"
        y2=".5"
      />
      <line
        class="c-easingEdit-thinLine"
        x1="0"
        y1=".75"
        x2="1"
        y2=".75"
      />
      <rect
        class="c-easingEdit-helpLine"
        x="0"
        y="0"
        width="1"
        height="1"
      />
      <g v-if="!isSteps">
        <line
          v-if="$store.state.gradient.ease1.x > 0 || $store.state.gradient.ease1.y > 0"
          :x2="$store.state.gradient.ease1.x"
          :y2="1 - $store.state.gradient.ease1.y"
          class="c-easingEdit-line"
          x1="0"
          y1="1"
        />
        <line
          v-if="$store.state.gradient.ease2.x < 1 || $store.state.gradient.ease2.y < 1"
          :x2="$store.state.gradient.ease2.x"
          :y2="1 - $store.state.gradient.ease2.y"
          class="c-easingEdit-line"
          x1="1"
          y1="0"
        />
      </g>
    </svg>
    <div
      v-if="!isSteps"
      :style="`left: ${$store.state.gradient.ease1.x * 100}%; top: ${100 - $store.state.gradient.ease1.y * 100}%`"
      class="u-knob"
      @mousedown="down($event, 'ease1')"
      @touchstart.prevent="down($event, 'ease1')"
    />
    <div
      v-if="!isSteps"
      :style="`left: ${$store.state.gradient.ease2.x * 100}%; top: ${100 - $store.state.gradient.ease2.y * 100}%`"
      class="u-knob"
      @mousedown="down($event, 'ease2')"
      @touchstart.prevent="down($event, 'ease2')"
    />
  </div>
</template>

<script>
import mouse from './mixins/mouse'
import misc from './mixins/misc'

export default {
  mixins: [mouse, misc],
}
</script>

<style>
.c-easingEdit {
  /* Placeholder */
}

.c-easingEdit-toggle {
  margin-top: var(--spacer-xsmall);
  margin-left: var(--spacer-xsmall);
}

.c-easingEdit-lines {
  overflow: visible;
  z-index: -1;
}

.c-easingEdit-line,
.c-easingEdit-helpLine {
  stroke-width: var(--stroke-medium);
  stroke-linecap: round;
  stroke-linejoin: round;
  vector-effect: non-scaling-stroke;
}

.c-easingEdit-line {
  stroke: var(--color-themed-fg);
}

.c-easingEdit-helpLine {
  stroke: var(--color-themed-fg-72);
  fill: none;
}

.c-easingEdit-thinLine {
  fill: none;
  stroke-width: var(--stroke-small);
  stroke: var(--color-themed-fg-72);
  vector-effect: non-scaling-stroke;
}
</style>
