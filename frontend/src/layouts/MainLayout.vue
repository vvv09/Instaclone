<template>
  <q-layout view="lHh Lpr lFf">
    <q-header
      class="bg-white text-grey-10"
    >
      <q-toolbar>
        <q-toolbar-title>
          Instaclone
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer
      bordered
      class="bg-white"
    >
      <q-tabs
        class="text-grey-10"
        active-color="primary"
        indicator-color="transparent"
      >
        <q-route-tab
          to="/"
          icon="eva-home-outline"
          name="home"
        />
        <q-route-tab
          to="/camera"
          icon="eva-camera-outline"
          name="camera"
        />
      </q-tabs>
    </q-footer>
  </q-layout>
</template>

<script setup>
</script>

<style lang="scss">

  .q-toolbar__title {
    text-align: center;
  }

  .q-footer {
    .q-tab__icon {
      font-size: 30px;
    }
  }

</style>
