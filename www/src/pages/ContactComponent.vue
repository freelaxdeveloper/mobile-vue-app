<template>
  <b-container class="bv-example-row">
    <div v-if="!device">No device</div>
    <div v-for="(contact, index) in contacts" :key="index">
      {{ contact.displayName }} (<span v-for="(phone, index2) in contact.phoneNumbers" :key="index2"> {{ phone.value }} </span>)
    </div>
  </b-container>
</template>

<script>
import { Contacts } from 'ionic-native';

export default {
  data() {
    return {
      contacts: [],
      device: false,
    }
  },
  created() {
    document.addEventListener("deviceready", () => {
      this.device = true
      Contacts.find(['emails', 'givenName', 'name', 'organizations', 'phoneNumbers'], {multiple: true}).then(
      (res) => {
        this.contacts = res;
      })
   }, false)
  },
}
</script>
