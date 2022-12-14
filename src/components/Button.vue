<template>
  <div
    :class="{
      'vue-scheduler-button-container': true,
      'vue-scheduler-button-container--arrow-left': arrowOnLeft,
    }"
  >
    <button
      v-if="label"
      :class="{
        'vue-scheduler-button': true,
        'vue-scheduler-button--link': typeIs('link'),
        'vue-scheduler-button--arrow': typeIs('arrow'),
      }"
    >
      {{ label }}
    </button>

    <ArrowIcon v-if="typeIs('arrow')" :size="arrowSize" :dir="arrowDir" />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

import { ButtonType, ArrowDirection } from '@/types';

import ArrowIcon from '@/components/ArrowIcon.vue';

export default defineComponent({
  name: 'Button',

  components: {
    ArrowIcon,
  },

  props: {
    label: String,

    type: {
      type: String as PropType<ButtonType>,
      default: 'link',
    },

    arrowSize: Number,

    arrowDir: String as PropType<ArrowDirection>,

    arrowOnLeft: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    typeIs(type: string): boolean {
      return this.type === type;
    },
  },
});
</script>

<style lang="scss" scoped>
.vue-scheduler-button-container {
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 4px;

  &--arrow-left {
    flex-direction: row-reverse;
  }

  &, .vue-scheduler-button {
    cursor: pointer;
  }
}

.vue-scheduler-button {
  background-color: transparent;
  border: none;
  outline: none;
  font-size: 12px;
  padding: 0px;
  
  &--link {
    text-decoration: underline;
  }
}
</style>
