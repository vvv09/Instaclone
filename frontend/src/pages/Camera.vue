<template>
  <q-page
    class="constrain-more q-pa-md"
  >
    <div
      class="camera-frame q-pa-md"
    >
      <img
        class="full-width"
        src="https://cdn.quasar.dev/img/mountains.jpg"
      >
    </div>
    <div
      class="text-center q-pa-md"
    >
      <q-btn
        size="lg"
        round
        color="grey-10"
        icon="eva-camera"
      />

      <div
        class="row justify-center q-ma-md"
      >
        <q-input
          dense
          v-model="post.caption"
          class="col col-sm-6"
          label="Caption"
        />
      </div>

      <div
        class="row justify-center q-ma-md"
      >
        <q-input
          dense
          v-model="post.location"
          class="col col-sm-6"
          label="Location"
        >
          <template
            v-slot:append
          >
            <q-btn
              round
              dense
              flat
              icon="eva-navigation-2-outline"
            />
          </template>
        </q-input>
      </div>

      <div
        class="row justify-center q-mt-lg"
      >
        <q-btn
          color="primary"
          label="Post Image"
          rounded
          unelevated
        />
      </div>

    </div>
  </q-page>
</template>

<script setup>
  import { ref } from 'vue'
  import { uid } from 'quasar'

  const post = ref({
    id: uid(), // TODO поудмать над тем чтобы перенесть создание id на бэк
    caption: 'test caption',
    location: 'test location',
    photo: null,
    date: Date.now() // TODO поудмать над тем чтобы перенесть создание таймштампа на бэкэнде()
  })
</script>


<style lang="scss">
  .camera-frame {
    border: 2px solid $grey-10;
    border-radius: 10px;
  }
</style>
