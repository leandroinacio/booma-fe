<template>
  <div class="input-validator">
    <InputValidator
      v-for="(word, index) in words"
      :key="word+index"
      :ref="'input-' + index"
      :word="word"
      :order="index"
      @textCompleted="changeFocus(index, 1)"
      @textDeleted="changeFocus(index, -1)"
      @keydown.native.left="changeFocus(index, -1)"
      @keydown.native.right.space="changeFocus(index, 1)"
    />
  </div>
</template>

<script>
import InputValidator from '~/components/form/InputValidator'

export default {
  components: {
    InputValidator
  },
  props: {
    text: {
      type: String,
      default: 'Oi, este é um teste do Leandro.'
    }
  },
  data () {
    return {
      textTyped: ''
    }
  },
  computed: {
    words () {
      return this.text.split(' ')
    }
  },
  methods: {
    changeFocus (index, indexChange) {
      const nextFieldIndex = Number(index) + Number(indexChange)

      if (this.words.length <= nextFieldIndex || nextFieldIndex < 0) {
        // TODO: Implement success - article completed.
        return
      }
      this.$nextTick(() => {
        this.$refs[`input-${nextFieldIndex}`][0].$el.children[0].focus()
      })
    }
  }
}
</script>

<style lang="scss">
</style>
