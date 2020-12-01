<template>
  <main>
    <section class="field mt-3">
      <label
        class="label is-unselectable"
        for="input"
      >
        Enter encrypted text:
      </label>
      <div class="control">
        <textarea
          class="textarea"
          id="input"
          placeholder="xjsy afu gzbt!"
          v-model="input"
        />
      </div>
    </section>
    <b class="is-unselectable">Replacements:</b>
    <br>
    <section class="is-flex is-flex-direction-row is-flex-wrap-wrap my-3">
      <div
        v-for="(repl, idx) in replacements"
        :key="idx"
        class="card mx-2 my-2"
      >
        <div class="card-content">
          <div class="field">
            <label
              class="label is-unselectable"
              :for="`old-char-${idx}`"
            >
              Character in original text:
            </label>
            <div class="control">
              <input
                type="text"
                size="3"
                maxlength="1"
                v-model="repl.old"
                :id="`old-char-${idx}`"
              >
            </div>
          </div>
          <div class="field">
            <label
              class="label is-unselectable"
              :for="`new-char-${idx}`"
            >
              Character as replacement:
            </label>
            <div class="control">
              <input
                type="text"
                size="3"
                maxlength="1"
                v-model="repl.new"
                :id="`new-char-${idx}`"
              >
            </div>
          </div>
          <button
            class="button is-danger is-small is-unselectable"
            @click="deleteReplacement(idx)"
          >
            Delete this
          </button>
        </div>
      </div>
    </section>
    <label class="checkbox is-block">
      <input
        type="checkbox"
        v-model="autoLowerUpperCase"
      >
      Auto-transform lower-case and upper-case
    </label>
    <button
      class="button is-primary my-2 is-unselectable"
      type="button"
      @click="addReplacement"
    >
      Add replacement
    </button>
    <section>
      <b class="my-3 is-inline-block is-unselectable">Result: </b>
      <br>
      <textarea
        class="textarea has-cursor-text"
        disabled
        rows="8"
        v-model="result"
      />
    </section>
  </main>
</template>

<script>
export default {
  name: 'TextReplacer',
  data () {
    return {
      input: '',
      replacements: [],
      autoLowerUpperCase: false
    }
  },
  methods: {
    addReplacement () {
      this.replacements.push({
        old: '',
        new: ''
      })
    },
    deleteReplacement (index) {
      this.replacements.splice(index, 1)
    }
  },
  computed: {
    result () {
      const inputArray = this.input.split('')
      const resultArray = new Array(inputArray.length).fill(0)
      const replacers = [...this.replacements]
      if (this.autoLowerUpperCase) {
        replacers.forEach(repl => {
          if (!replacers.includes({
            old: repl.old.toLowerCase(),
            new: repl.new.toLowerCase()
          })) {
            replacers.push({
              old: repl.old.toLowerCase(),
              new: repl.new.toLowerCase()
            })
          }
          if (!replacers.includes({
            old: repl.old.toUpperCase(),
            new: repl.new.toUpperCase()
          })) {
            replacers.push({
              old: repl.old.toUpperCase(),
              new: repl.new.toUpperCase()
            })
          }
        })
      }
      replacers.forEach(repl => {
        const places = inputArray.reduce((acc, value, index) => {
          if (value === repl.old) {
            acc.push(index)
          }
          return acc
        }, [])
        places.forEach(place => {
          resultArray[place] = repl.new
        })
      })
      return resultArray.map((value, index) => {
        if (value === 0) {
          return inputArray[index]
        }
        return value
      }).join('')
    }
  }
}
</script>

<style>
.has-cursor-text {
  cursor: text !important;
  pointer-events: all;
}
</style>
