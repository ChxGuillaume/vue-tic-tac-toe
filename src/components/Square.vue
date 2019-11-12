<template>
  <div id="square">
    <fa-icon class="red" :icon="['fas', 'times']" v-if="value === 0"></fa-icon>
    <fa-icon class="green" :icon="['far', 'circle']" v-else-if="value === 1"></fa-icon>

    <fa-icon class="onHover red" :icon="['fas', 'times']"
             v-if="whoPlay === 0 && value === -1"></fa-icon>
    <fa-icon class="onHover green" :icon="['far', 'circle']"
             v-else-if="whoPlay === 1 && value === -1"></fa-icon>
  </div>
</template>

<script>
export default {
  name: 'Square',
  props: {
    whoPlay: {
      type: Number,
      required: true,
    },
    value: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
  #square {
    width: 100%;
    height: 100%;

    &:hover {
      .red {
        &.onHover {
          color: rgba(244, 67, 54, 0.5);
        }
      }

      .green {
        &.onHover {
          color: rgba(76, 175, 80, 0.5);
        }
      }
    }

    svg {
      position: absolute;
      top: 0;
      bottom: 0;
      left: 0;
      right: 0;
      margin: auto;

      &.red {
        color: #f44336;
      }

      &.green {
        color: #4CAF50;
      }

      &.onHover {
        color: rgb(0, 0, 0, 0);
        transition: .2s ease;
      }
    }
  }
</style>
