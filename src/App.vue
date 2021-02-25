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
        <input v-model="infoUser.name" type="text" id="name">
        <small v-show="!checkFilledFields.name">blank field!</small>
        <label for="email">Email:</label>
        <input v-model="infoUser.email" type="email" id="email">
        <small v-show="!checkFilledFields.email">blank field!</small>
      </div>
      <div class="step2" v-if="activeTab === 2">
        <label for="number">Number:</label>
        <input v-model="infoUser.number" type="text" id="number">
        <small v-show="!checkFilledFields.number">blank field!</small>
        <label for="address">Address:</label>
        <input v-model="infoUser.address" type="email" id="address">
        <small v-show="!checkFilledFields.address">blank field!</small>
      </div>
      <div class="step2" v-if="activeTab === 3">
        <small v-show="!this.checkConfirmPassword">Password is different</small>
        <label for="password">Password:</label>
        <input type="password" v-model="infoUser.password" id="password">
        <small v-show="!checkFilledFields.password">blank field!</small>
        <label for="passwordConfirm">Confirm password:</label>
        <input type="password" v-model="infoUser.password2" id="passwordConfirm">
        <small v-show="!checkFilledFields.password2">blank field!</small>
      </div>
      <input type="button" :value="activeTab === 3 ? 'FINISH' : 'NEXT' " @click="checkStepFilled">
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
      infoUser: {
        name: '',
        email: '',
        number: '',
        address: '',
        password: '',
        password2: ''
      },
      checkFilledFields:{
        name: true,
        email: true,
        number: true,
        address: true,
        password: true,
        password2: true
      }
    }
  },
  computed: {
    checkConfirmPassword () {
      return (this.infoUser.password === this.infoUser.password2)
    }
  },
  methods: {
    checkStepFilled () {
     if (this.activeTab === 1) {
       this.checkFilledFields.name = !!this.infoUser.name
       this.checkFilledFields.email = !!this.infoUser.email
       return this.checkFilledFields.name && this.checkFilledFields.email && this.activeTab++
     } else if (this.activeTab === 2) {
       this.checkFilledFields.number = !!this.infoUser.number
       this.checkFilledFields.address = !!this.infoUser.address
       return this.checkFilledFields.number && this.checkFilledFields.address && this.activeTab++
     } else if (this.activeTab === 3) {
       this.checkFilledFields.password = !!this.infoUser.password
       this.checkFilledFields.password2 = !!this.infoUser.password2
       return this.checkConfirmPassword && this.checkFilledFields.password && this.checkFilledFields.password2  && alert(`Hello ${this.infoUser.name}`)
     }

    }
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
      small{
        color: #e21515;
      }
      input{
        &[type="button"]{
          width: 30%;
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
