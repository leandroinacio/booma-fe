<template>
  <div
    class="input-validator"
    :class="{ 'input-validator--focused': isFocused }"
  >
    <input
      v-model="textTyped"
      :style="automaticWidth"
      type="text"
      class="input-validator__field"
      @focus="isFocused=true"
      @blur="isFocused=false"
      @keydown.backspace="navigateBack"
    >
    <PlaceholderWord
      :word="word"
      :state="state"
      class="input-validator__placeholder"
    />
  </div>
</template>

<script>
import PlaceholderWord, { STATES } from '~/components/form/PlaceholderWord'

export default {
  components: {
    PlaceholderWord
  },
  props: {
    word: {
      type: String,
      default: ''
    },
    order: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      isFocused: false,
      textTyped: ''
    }
  },
  computed: {
    // Return the list of words required for this line broken down into a list with a status for each word based on what was typed
    state () {
      if (!this.textTyped.length) { return STATES.IDLE }
      if (this.textTyped.length < this.word.length && this.isFocused) { return STATES.IN_PROGRESS }
      if (this.textTyped.toLocaleLowerCase().trim() === this.word.toLocaleLowerCase().trim()) { return STATES.CORRECT }
      return STATES.INCORRECT
    },
    automaticWidth () {
      return { width: `${this.word.length}rem` }
    }
  },
  watch: {
    state (newValue) {
      if (newValue === STATES.CORRECT) { this.$emit('textCompleted') }
    }
  },
  methods: {
    navigateBack () {
      if (this.textTyped.length === 0) {
        this.$emit('textDeleted')
      }
    }
  }
}
</script>

<style lang="scss">
.input-validator {
  position: relative;
  display: inline;
  outline: 0;

  &__field {
    position: relative;
    border: none;
    outline: 0;
  }
  &__placeholder {
    position: absolute;
    top: 0;
    left: 0;
    transition: ease .3s;

    &.placeholder-word--correct {
      top: 100%
    }
    &.placeholder-word--incorrect {
      background: red, 0.5;
      top: 100%
    }
    &.placeholder-word--in-progress {
      top: 100%
    }
  }
  &--focused {
    .input-validator__placeholder {
      top: 100%;
    }
  }
}
</style>
