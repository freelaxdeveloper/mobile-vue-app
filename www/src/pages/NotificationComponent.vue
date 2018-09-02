<template>
  <b-container class="bv-example-row">
    <button class="btn" @click="alert">alert</button>
    <button class="btn" @click="confirm">confirm</button>
    <button class="btn" @click="prompt">prompt</button>
    <button class="btn" @click="beep">beep</button>
    <button class="btn" @click="vibrate">Vibrate</button>
    
    <div class="row">
      <div class="col-md-4">
        <b-row class="my-1">
          <b-col sm="2"><label for="input-small">Vibrate:</label></b-col>
          <b-col sm="10">
            <b-form-input id="input-small" size="sm" type="text" v-model="duration"></b-form-input>
          </b-col>
        </b-row>
        <b-row class="my-1">
          <b-col sm="2"><label for="input-small">Beep:</label></b-col>
          <b-col sm="10">
            <b-form-input id="input-small" size="sm" type="text" v-model="countBeep"></b-form-input>
          </b-col>
        </b-row>
      </div>
    </div>
    
    

    <div v-if="name">
      {{ name }}
    </div>
  </b-container>
</template>

<script>

export default {
  data() {
    return {
      duration: 250,
      countBeep: 1,
      name: '',
    }
  },
  methods: {
   alert() {
      document.addEventListener("deviceready", () => {
        navigator.notification.alert(
          'You are the winner!',
          () => {
            this.$router.push('/')
          },
          'Game Over',
          'Done'
        )
      }, false);
      console.log('alert')
    },
    confirm() {
      document.addEventListener("deviceready", () => {
        navigator.notification.confirm(
          'You are the winner!',
          (buttonIndex) => {
            if (buttonIndex == 1) {
              this.$router.push('/')
            } else if (buttonIndex == 2) {
              this.$router.push('/news')
            } else if (buttonIndex == 3) {
              this.$router.push('/notification')
            }
          },
          'Game Over',
          ['Home','News','Notifications']
        )
      }, false);
      console.log('confirm')
    },
    prompt() {
      document.addEventListener("deviceready", () => {
        navigator.notification.prompt(
          'Please enter your name',
          (results) => {
            if (results.buttonIndex == 1) {
              this.name = results.input1
            } else if (results.buttonIndex == 2) {
              
            }
          },
          'Registration',
          ['Ok','Exit'],
          this.name
        )
      }, false);
      console.log('prompt')
    },
    beep() {
      document.addEventListener("deviceready", () => {
        navigator.notification.beep(this.countBeep)
      }, false)
      console.log('beep')
    },
    vibrate() {
      navigator.vibrate([this.duration])
      console.log('vibrate', this.duration)
    },
  }
}
</script>
