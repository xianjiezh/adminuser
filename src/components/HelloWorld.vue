<template>
  <div class="hello">
    <div v-if="!haveData">
      密码：<input type="password" v-model="passWord">
      <button @click="login">登陆</button>
    </div>
    <ul v-if="haveData">
      <li v-for="user in users">
        <div>
          电话： {{user.phone}} 参赛码： {{user.attendanceNumber}} 是否签到： {{user.status}}
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      haveData: false,
      users: [],
      passWord: ''
    }
  },
  methods: {
    login() {
      this.axios
        .get('https://gjs.so/wxgameapp/adminusermsg?password=' + this.passWord)
        .then(res => {
          this.haveData = true
          this.users = res.data
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
