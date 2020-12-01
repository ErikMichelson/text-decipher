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
@import '~bulma/sass/utilities/all';
@import '~bulma/sass/base/all';
@import '~bulma/sass/components/card';
@import '~bulma/sass/elements/button';
@import '~bulma/sass/elements/container';
@import '~bulma/sass/elements/title';
@import '~bulma/sass/form/shared';
@import '~bulma/sass/form/input-textarea';
@import '~bulma/sass/form/tools';
@import '~bulma/sass/helpers/spacing';
@import '~bulma/sass/helpers/flexbox';
@import '~bulma/sass/helpers/visibility';
@import '~bulma/sass/layout/hero';
@import '~bulma/sass/helpers/other';
</style>
