<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="q-pt-md q-px-lg">
      <q-toolbar>
        <q-toolbar-title>
          <div class="logo q-ml-xl">
            <img src="./../assets/logo.png" alt="Logo Search and Stay" />
          </div>
        </q-toolbar-title>
        <q-avatar v-if="loggedIn">
          <img src="https://cdn.quasar.dev/img/avatar.png" />
        </q-avatar>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainLayout',
  data() {
    return {
      loggedIn: localStorage.getItem('token'), // Default value if not found in local storage
    };
  },
});
</script>

<style scoped>
.q-layout__section--marginal {
  background-color: white;
  color: #667085;
}
</style>
