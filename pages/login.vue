<template>
  <div class="flex flex-col  items-center my-4 mx-auto w-4/5 border rounded-md">
    <label class="font-bold">e-mail
      <input id="email" v-model="user.email" class="border mt-4 p-1" type="text" name="email" />
    </label>
    <label class="font-bold">senha
      <input id="senha" class="border mt-4 p-1" type="password" name="senha" />
    </label>
    <div class="flex justify-center w-4/5 m-2 ">
        <nuxt-link 
          to="/"
          class="w-32 m-2 p-2 rounded-lg bg-blue-400 text-center text-white"
        >Login</nuxt-link>
        <button
          class="w-32 m-2 p-2 rounded-lg border"
          @click="cancelar"
        >Cancelar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginPage',
  // layout: 'no-nav'

  async fetch() {
    return await this.$axios
      .get('http://localhost:5000/users')
      .then((response) => {
        this.$store.dispatch('setUser', response.data[0])
      })
  },
  head() {
    return {
      title: 'Login Page',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'test description on component',
        },
      ],
    }
  },

  computed:{
    user(){
      return this.$store.state.user;
    }
  },

  methods: {
    cancelar(){
      this.$store.dispatch('setUser', {});
      this.$router.push('/');
    }
  }
}
</script>
