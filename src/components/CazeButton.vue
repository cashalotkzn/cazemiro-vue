<template>
  <button
      class="caze-button"
      :disabled="disabled"
      :class="computedClass">
    <span class="caze-button__content">
      <span v-if="$slots.before"
            class="caze-button__content_inner_before">
        <slot name="before"/>
      </span>
      <slot />
      <span v-if="$slots.after"
            class="caze-button__content_inner_after">
        <slot name="after"/>
      </span>
    </span>
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  block?: boolean,
  disabled?: boolean,
  color?: string,
  shadow?: boolean,
  gradient?: boolean,
  circle?: boolean,
  square?: boolean
}

interface ComputedClass {
  'caze-button_block': boolean | undefined
  'caze-button_shadow': boolean | undefined
  'caze-button_gradient': boolean | undefined
  'caze-button_square': boolean | undefined
  'caze-button_circle': boolean | undefined
}

// eslint-disable-next-line vue/no-setup-props-destructure
const {
  block = false,
  disabled = false,
  shadow = false,
  gradient = false,
  square = false,
  circle = false,
  color = 'primary'
} = defineProps<Props>()
const computedClass = computed<ComputedClass>(() => {
  const computedClass = {
    'caze-button_block': block,
    'caze-button_shadow': shadow,
    'caze-button_gradient': gradient,
    'caze-button_square': square,
    'caze-button_circle': circle
  }

  // eslint-disable-next-line @typescript-eslint/ban-ts-comment
  // @ts-ignore
  computedClass[`caze-button_color_${color}`] = true

  return computedClass
})
</script>

<style scoped lang="scss">
  @import "../scss/buttons";

  .caze-button {
    padding: $buttons-padding;
    border-radius: $buttons-border-radius;
    border: $buttons-border;
    cursor: $buttons-cursor;
    transition: $buttons-transition;
    position: relative;
    overflow: hidden;
    color: #fff;

    &:disabled {
      cursor: $buttons-cursor_disabled;
    }

    &:active {
      transform: $buttons-transform_active;
    }

    &:hover {
      opacity: 0.8;
    }

    &_block {
      display: block;
      width: 100%;
    }

    &__content {
      position: relative;
      z-index: 1;
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    &_gradient {
      &::before {
        content: "";
        background: linear-gradient(
                30deg,rgba(var(--cz-color),0) 33%,rgba(var(--cz-color),1));
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        -webkit-filter: hue-rotate(
                -40deg);
        filter: hue-rotate(
                -40deg);
      }
    }
  }
</style>
