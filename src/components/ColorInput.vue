<template>
    <app-icon class="picker"
              type="color"
              :big="big"
              @mouseenter.native="togglePicker(true)"
              @mouseleave.native="togglePicker()">
        <transition name="picker">
            <div v-if="showColorPicker"
                 class="picker__wrapper">
                <div class="picker__color"
                     v-for="(hex, name) in colors"
                     :key="hex"
                     :style="'background-color: var(--' + name + ')'"
                     @click="$emit('change', name)">
                </div>
            </div>
        </transition>
    </app-icon>
</template>

<script>
import AppIcon from './AppIcon.vue';
import colors from '../colorConfig';

export default {
  name: 'ColorInput',
  components: {
    AppIcon,
  },
  props: {
    big: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      showColorPicker: false,
      colors,
    };
  },
  methods: {
    togglePicker(show) {
      this.showColorPicker = show;
    },
  },
};
</script>

<style lang="scss" scoped>
    @import "../style/variables";

    .picker {
        position: relative;

        &__wrapper {
            position: absolute;
            top: 100%;
            width: 128px;
            padding: 4px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            background-color: $main-dark;
            box-shadow: 0 1px 4px rgba(0, 0, 0, 0.2);
            cursor: default;
            transition: .2s;
            z-index: 1;
        }

        &__color {
            width: 22px;
            height: 22px;
            margin: 2px;
            border-radius: 50%;
            border: 1px solid $border-color;
            cursor: pointer;
            transition: .2s;

            &:hover {
                border: 1px solid lighten($border-color, 20%);
            }
        }
    }

    .picker-enter-active,
    .picker-leave-active {
        opacity: 1;
    }

    .picker-enter,
    .picker-leave-to {
        opacity: 0;
    }
</style>
