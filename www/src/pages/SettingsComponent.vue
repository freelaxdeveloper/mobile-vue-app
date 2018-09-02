<template>
  <b-container class="bv-example-row">
    <button :class="`btn btn-${buttonClass}`" @click="toggleStatusBar">Переключить Status Bar</button>
 </b-container>
</template>

<script>
export default {
  computed: {
    statusbar() {
      return this.$store.state.settings.statusbar
    },
    buttonClass() {
      return this.statusbar ? 'success' : 'danger'
    },
  },
  methods: {
    toggleStatusBar() {
      this.$store.dispatch('toggleStatusBar')
    }
  }
}
</script>
