<template>
  <div>
    <form @submit.prevent="signUp">
      <input v-model="email" type="text" placeholder="email" name="email" />
      <input
        v-model="password"
        type="text"
        placeholder="password"
        name="password"
      />
      <button type="submit">signup</button>
    </form>
    <div v-if="show">{{ message }}</div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { auth } from '@/lib/firebase/client'
export default Vue.extend({
  data() {
    return {
      email: '' as string,
      password: '' as string,
      show: false as boolean,
      message: '' as string,
    }
  },
  methods: {
    signUp() {
      auth
        .createUserWithEmailAndPassword(this.email, this.password)
        .then((data) => {
          console.log(data)
        })
        .catch((err) => {
          this.message = `${err.code} : ${err.message}`
          this.show = true

          setTimeout(() => {
            this.show = false
          }, 3000)
        })
    },
  },
})
</script>
