<template>
  <article class="container">
    <section class="quiz align-items-center">
      <div class="text-center">
        <h2>
          Quiz : <span class="orange">{{ qNumber + 1 }} </span>/
          {{ que.length }}
        </h2>
        <Counter />
        <hr />
      </div>
      <div>
        <div class="q">
          <span class="orange">Q)</span>
          <span v-html="q" />
        </div>

        <ul class="list-group mt-2 px-2 text-capitalize">
          <li id="a" class="list-group-item" @click="answer('a')">
            <span class="answer text-center">A</span> {{ a }}
          </li>
          <li id="b" class="list-group-item" @click="answer('b')">
            <span class="answer text-center">B</span> {{ b }}
          </li>
          <li
            v-show="c !== ''"
            id="c"
            class="list-group-item"
            @click="answer('c')"
          >
            <span class="answer text-center">C</span>{{ c }}
          </li>
          <li
            v-show="d !== ''"
            id="d"
            class="list-group-item"
            @click="answer('d')"
          >
            <span class="answer text-center">D</span>{{ d }}
          </li>
        </ul>
      </div>
      <div class="row container mt-2">
        <button
          type="button"
          class="btn btn-success mx-1 text-center col-5"
          :disabled="choose || value == 'null'"
          @click="submit()"
        >
          Submit
        </button>

        <button
          type="button"
          class="btn btn-custom mx-1 text-center col-5"
          :disabled="choose == false"
          @click="next()"
        >
          Next
        </button>
      </div>
    </section>
  </article>
</template>

<script>
import { Que } from '~/assets/js/os.js'
export default {
  data() {
    return {
      choose: false,
      value: 'null',
      q: '',
      que: Que,
      a: '',
      b: '',
      c: '',
      d: '',
      result: '',
      mark: null,
      qNumber: 0,
    }
  },
  created() {
    if (this.$route?.query?.random) this.que = this.shuffle(this.que)
  },
  mounted() {
    const q1 = this.que[this.qNumber]
    this.q = q1.q
    this.a = q1.a
    this.b = q1.b
    this.c = q1.c
    this.d = q1.d
    this.result = q1.Answer
  },
  methods: {
    answer(id) {
      const ele = document.querySelectorAll('.list-group-item')

      ele.forEach((element) => {
        element.classList.remove('active')
      })

      document.getElementById(id).classList.add('active')
      this.value = `${id}`
    },
    submit() {
      this.choose = true

      if (this.value === this.result) {
        document.getElementById(this.value).classList.remove('active')
        document.getElementById(this.value).classList.add('true')
        this.mark = this.mark + 1
      } else {
        document.getElementById(this.value).classList.remove('active')
        document.getElementById(this.result).classList.add('true')
        document.getElementById(this.value).classList.add('false')
      }
    },
    next() {
      this.choose = false
      document.getElementById(this.value).classList.remove('active')
      document.getElementById(this.result).classList.remove('true')
      document.getElementById(this.value).classList.remove('false')
      this.qNumber++
      this.value = 'null'

      if (this.qNumber === this.que.length)
        this.$router.push(`/result/${this.mark}`)

      const q1 = this.que[this.qNumber]

      this.q = q1.q
      this.a = q1.a
      this.b = q1.b
      this.c = q1.c
      this.d = q1.d
      this.result = q1.Answer
    },
    shuffle(array) {
      return array.sort(() => Math.random() - 0.5)
    },
  },
}
</script>
