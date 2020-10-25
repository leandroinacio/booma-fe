<template>
  <span :class="wordClass" v-text="word" />
</template>

<script>
export const STATES = {
  IDLE: 'idle',
  CORRECT: 'correct',
  INCORRECT: 'incorrect',
  IN_PROGRESS: 'in-progress'
}

export default {
  name: 'PlaceholderWord',
  props: {
    word: {
      type: String,
      default: ''
    },
    state: {
      type: String,
      default: STATES.IDLE,
      validator: state => Object.values(STATES).includes(state)
    }
  },
  computed: {
    wordClass () {
      return `placeholder-word--${this.state}`
    }
  }
}
</script>

<style lang="scss">
.placeholder-word {
  &--idle {
    opacity: .8;
    color: black;
    padding: 0 5px 0 0;
  }
  &--correct {
    color: green;
    padding: 0 5px 0 0;
  }
  &--incorrect {
    color: red;
    padding: 0 5px 0 0;
  }
  &--in-progress {
    color: orange;
    padding: 0 5px 0 0;
  }
}
</style>
