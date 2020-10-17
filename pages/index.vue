<template>
  <section class="container">
    <div class="container max-w-xl mx-auto pt-6">
      <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
        <div class="mb-4">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="myLine"
          >
            なにか入力欄
          </label>
          <input
            id="myLine"
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            type="text"
            placeholder="なにかを入力してください"
            @input="changeLine"
          />
        </div>
        <div class="mb-4 pt-5">
          <label class="block text-gray-700 text-sm font-bold mb-2">
            なにかの候補
          </label>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import Vue from 'vue'
import _ from 'lodash'

export type DataType = {
  line: string | null
}

export default Vue.extend({
  data(): DataType {
    return {
      line: '',
    }
  },
  watch: {
    // eslint-disable-next-line @typescript-eslint/no-unused-vars
    line(newLine, oldLine): void {
      this.searchWithInterval()
    },
  },
  created(): void {
    this.searchWithInterval = _.throttle(this.search, 500)
  },
  methods: {
    searchWithInterval(): void {},
    changeLine(): void {
      // HTMLElementにはvalueプロパティがないため、HTMLElementを継承したHTMLInputElementで型アサーション
      this.line = (document.getElementById('myLine') as HTMLInputElement).value
    },
    search(): void {
      if (!this.line) return
      // TODO: do something
      console.log(this.line)
    },
  },
})
</script>
