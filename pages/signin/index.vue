<template>
  <div class="container">
    <!-- <OAuthSignInButton></OAuthSignInButton> -->
    <form @submit.prevent="signIn">
      <input v-model="email" type="text" placeholder="email" name="email" />
      <input
        v-model="password"
        type="text"
        placeholder="password"
        name="password"
      />
      <button type="submit">signin</button>
    </form>
    <div v-show="noUser">{{ message }}</div>
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
      noUser: false as boolean,
      message: '' as string,
    }
  },
  methods: {
    signIn() {
      console.log('signin')
      auth
        .signInWithEmailAndPassword(this.email, this.password)
        .then((data) => {
          console.log(data)
          this.email = ''
          this.password = ''
        })
        .catch((err) => {
          console.log(`error_code: ${err.code}`, `error_msg: ${err.message}`)
          this.message = `${err.code} : ${err.message}`
          this.noUser = true
          const that = this
          setTimeout(function () {
            that.noUser = false
          }, 3000)
        })
    },
  },
})
</script>
