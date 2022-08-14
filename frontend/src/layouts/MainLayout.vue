<template>
  <q-layout view="lHh Lpr lFf">
    <q-header
      bordered
      class="bg-white text-grey-10"
    >
      <q-toolbar
        class="constrain"
      >
        <q-btn
          v-if="$q.screen.gt.sm"
          to="/"
          flat
          round
          dense
          size="18px"
          class="q-mr-sm"
          icon="eva-home-outline"
        />
        <q-separator
          v-if="$q.screen.gt.sm"
          vertical
          spaced
        />
        <q-toolbar-title
          class="text-grand-hotel text-bold"
        >
          Instaclone
        </q-toolbar-title>

        <q-btn
          v-if="$q.screen.gt.sm"
          to="/camera"
          flat
          round
          dense
          size="18px"
          icon="eva-camera-outline"
        />
      </q-toolbar>
    </q-header>

    <q-page-container class="bg-grey-1">
      <router-view />
    </q-page-container>

    <q-footer
      v-if="$q.screen.lt.md"
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

  .q-toolbar {
    @media (min-width: $breakpoint-md-min) {
      height: 77px;
    }
  }

  .q-toolbar__title {
    font-size: 30px;
    @media (max-width: $breakpoint-md-min) {
      text-align: center;
    }
  }

  .q-footer {
    .q-tab__icon {
      font-size: 30px;
    }
  }

</style>
