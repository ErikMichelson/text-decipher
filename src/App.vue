<template>
  <div id="app">
    <PageHeader />
    <div class="container">
      <TextReplacer />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import PageHeader from '@/layout/PageHeader.vue'
import TextReplacer from '@/components/TextReplacer.vue'

@Component({
  components: {
    TextReplacer,
    PageHeader
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import '~bulma/bulma.sass';
</style>
