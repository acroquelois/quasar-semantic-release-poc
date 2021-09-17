<template>
  <q-page class="flex flex-center">
    <div class="column items-center q-col-gutter-md">
      <img
        alt="Quasar logo"
        src="~assets/quasar-logo-vertical.svg"
        style="width: 200px; height: 200px"
      >
      <span>version: {{envVersion}}</span>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  setup() {
    return{
      envVersion : process.env.QUASAR_APP_VERSION
    }
  }
})
</script>
