<template>
  <main>
    <section class="field mt-3">
      <label
        class="label"
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
    <b>Replacements:</b>
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
              class="label"
              :for="`old-char-${idx}`"
            >
              Character in original text:
            </label>
            <div class="control">
              <input
                type="text"
                size="3"
                v-model="repl.old"
                :id="`old-char-${idx}`"
              >
            </div>
          </div>
          <div class="field">
            <label
              class="label"
              :for="`new-char-${idx}`"
            >
              Character as replacement:
            </label>
            <div class="control">
              <input
                type="text"
                size="3"
                v-model="repl.new"
                :id="`new-char-${idx}`"
              >
            </div>
          </div>
          <button
            class="button is-danger is-small"
            @click="deleteReplacement(idx)"
          >
            Delete this
          </button>
        </div>
      </div>
    </section>
    <button
      class="button is-primary my-2"
      type="button"
      @click="addReplacement"
    >
      Add replacement
    </button>
    <section>
      <b>Result: </b>
      <br>
      {{ result }}
    </section>
  </main>
</template>

<script>
export default {
  name: 'TextReplacer',
  data () {
    return {
      input: '',
      replacements: []
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
      this.replacements.forEach(repl => {
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
      console.debug(resultArray)
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

<style scoped>

</style>
