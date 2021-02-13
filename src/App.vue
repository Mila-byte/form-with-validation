<template>
  <div id="app">
    <ul>
      <li :class="{active: activeTab === 1, done: activeTab > 1}"></li>
      <li :class="{active: activeTab === 2, done: activeTab > 2}"></li>
      <li :class="{active: activeTab === 3, done: activeTab > 3}"></li>
    </ul>
    <div class="info">
      <div class="step1" v-if="activeTab === 1">
        <label for="name">Name:</label>
        <input type="text" id="name">
        <label for="email">Email:</label>
        <input type="email" id="email">
      </div>
      <div class="step2" v-if="activeTab === 2">
        <label for="number">Number:</label>
        <input type="text" id="number">
        <label for="adress">Adress:</label>
        <input type="email" id="adress">
      </div>
      <div class="step2" v-if="activeTab === 3">
        <label for="password">Password:</label>
        <input type="password" v-model="password" id="password">
        <label for="passwordConfirm">Confirm password:</label>
        <input type="password" v-model="password2" id="passwordConfirm">
      </div>
      <input type="button" :value="activeTab === 3 ? 'FINISH' : 'NEXT' " @click="changeState">
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data () {
    return {
      activeTab: 1,
      password: '',
      password2: ''
    }
  },
  computed: {
    checkConfirmPassword () {
      return (this.password === this.password2)
    },
    checkAllFields () {
      return this.password
    }
  },
  methods: {
    changeState () {
      if (this.activeTab === 3) {
       if (this.checkConfirmPassword && this.checkAllFields) {
         console.log('password is true')
       } else {
         console.log('password is false')
       }
      } else {
        this.activeTab++
      }
    },
  }
}
</script>

<style lang="scss">
@import "assets/reset.css";
#app {
  .info{
    max-width: 400px;
    margin: 0 auto;
    .step1, .step2 {
      display: flex;
      flex-direction: column;
      input{
        margin: 15px 0;
        &[type="button"]{
          width: 20%;
        }
      }
    }
  }
ul {
  display: flex;
  justify-content: center;
  li{
    list-style: none;
    width: 50px;
    height: 50px;
    background: #808080;
    margin: 5px;
    border-radius: 50%;
    &.done {
      background: #00008b;
    }
    &.active {
      border: 2px solid #00008b;
      box-sizing: border-box;
    }
  }
}
}
</style>
