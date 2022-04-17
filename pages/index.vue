<template>
<div class="bg-white min-h-full px-4 py-16 sm:px-6 sm:py-24 md:grid md:place-items-center lg:px-8">
  <div class="max-w-max mx-auto">
    <main class="sm:flex">
      <p class="text-4xl font-extrabold text-indigo-600 sm:text-5xl">Welcome</p>
      <div class="sm:ml-6">
        <div class="sm:border-l sm:border-gray-200 sm:pl-6">
          <h1 class="text-4xl font-extrabold text-gray-900 tracking-tight sm:text-5xl">{{data.email}}</h1>
          <p class="mt-1 text-base text-gray-500">This is simple app using Nuxt, Tailwind & Firebase</p>
        </div>
      </div>
    </main>
  </div>
</div>
</template>

<script>
import * as firebase from 'firebase/app'
import 'firebase/auth'
import { getUserFromCookie, getUserFromSession } from '@/helpers'
export default {
  data() {
    return {
      data: firebase.auth().currentUser
    }
  },
  asyncData({ req, redirect }) {
    if (process.server) {
      const user = getUserFromCookie(req)
      
      if (!user) {
        redirect('/login')
      }
    } else {
      var user = firebase.auth().currentUser
      console.log(user.refreshToken);
      if (!user) {
        redirect('/login')
      }
    }
  }
}
</script>
