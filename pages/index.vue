<template>
  <div>
    Shows list of most popular, new books, last ones accessed, favorite list...
    <br>
    <LineArea :text="text" />
  </div>
</template>

<script>
import LineArea from '~/components/form/LineArea'

export default {
  components: {
    LineArea
  },
  data () {
    return {
      text: 'Wayne went to wales to watch walruses.'
    }
  }
}
</script>

<style>
</style>
