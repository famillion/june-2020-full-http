<template>
  <div>
    <h1>HTTP Lesson</h1>
    <div>
      <label>Username</label>
      <input type="text" v-model="user.userName">
    </div>
    <div>
      <label>Email</label>
      <input type="email" v-model="user.email">
    </div>
    <button @click="submitData">Submit</button>
    <button @click="getUsers">Get users</button>
    <button @click="deleteUser">Delete user</button>
    <button @click="updateUser">Update user</button>
    <hr>
    <ul>
      <li v-for="(user, i) in users" :key="i">
        {{user}}
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
      user: {
        userName: '',
        email: ''
      },
      users: [],
    }
  },

  methods: {
    submitData() {
      // this.$http.post('http://localhost/users', this.user);
      // this.$http.post('https://http-lesson-vue.firebaseio.com/users.json', this.user)
      // .then((res) => {
      //   console.log(res);
      // }, error => {
      //   console.log(error)
      // })
      this.$http.post(`users.json`, this.user)
          .then((res) => {
            console.log(res);
          });
    },

    getUsers() {
      this.$http.get('users.json')
      .then((res) => {
        console.log(res, 'RESPONSE');
        return res.json()
      }).then((res) => {
        console.log(res, 'JSON');
        Object.values(res).forEach(u => this.users.push(u));
      })
    },

    deleteUser() {
      // this.$http.delete(`https://http-lesson-vue.firebaseio.com/${id}`)
      this.$http.delete('users.json')
      .then((res) => {
        console.log(res, 'DELETE');
      });
    },

    updateUser() {
      this.$http.put('-MFamzam49v-kBz1r_kw.json', {
        userName: 'name',
        email: 'email',
        id: '33',
        job: 'seniour'
      }).then((res) => {
        console.log(res, 'UPDATE');
      })
    }
  }
}
</script>

<style>
</style>
