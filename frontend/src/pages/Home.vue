<template>
  <q-page
    class="constrain q-pa-md"
  >
    <div
      class="row q-col-gutter-lg"
    >
      <div
        class="col-12 col-md-8"
      >
        <q-card
          v-for="post in posts"
          :key="post.id"
          class="card-post q-mb-md"
          flat
          bordered
        >
          <q-item>
            <q-item-section
              avatar
            >
              <q-avatar>
                <img
                  src="https://ru.gravatar.com/userimage/208843598/90c840a328857c5b73bf836e41c77c12.jpg?size=200"
                >
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label
                class="text-bold"
              >
                vadim__valunskii
              </q-item-label>

              <q-item-label
                caption
              >
                {{ post.location }}
              </q-item-label>
            </q-item-section>
          </q-item>

          <q-separator />

          <img
            :src="post.imageUrl"
          >

          <q-card-section>
            <div>
              {{ post.caption }}
            </div>
            <div
              class="text-caption text-grey"
            >
              {{ niceDate(post.date) }}
            </div>
          </q-card-section>
        </q-card>
      </div>
      <div
        v-if="$q.screen.gt.sm"
        class="col-4"
      >
        <q-item
          class="fixed"
        >
          <q-item-section
            avatar
          >
            <q-avatar
              size="48px"
            >
              <img
                src="https://ru.gravatar.com/userimage/208843598/90c840a328857c5b73bf836e41c77c12.jpg?size=200"
              >
            </q-avatar>
          </q-item-section>

          <q-item-section>
            <q-item-label
              class="text-bold"
            >
              vadim__valunskii
            </q-item-label>

            <q-item-label
              caption
            >
              Vadim Valunskii
            </q-item-label>
          </q-item-section>
        </q-item>
      </div>
    </div>
  </q-page>
</template>

<script setup>

  import { ref } from 'vue'
  import { date } from 'quasar'

  const posts = ref([
    {
      id: 1,
      caption: 'Nice Mountains',
      date: 1660473384846,
      location: 'Saint Petersburg, Russia',
      imageUrl: 'https://cdn.quasar.dev/img/mountains.jpg'
    },
    {
      id: 2,
      caption: 'Nice Mountains',
      date: 1660473384846,
      location: 'Saint Petersburg, Russia',
      imageUrl: 'https://cdn.quasar.dev/img/mountains.jpg'
    },
    {
      id: 3,
      caption: 'Nice Mountains',
      date: 1660473384846,
      location: 'Saint Petersburg, Russia',
      imageUrl: 'https://cdn.quasar.dev/img/mountains.jpg'
    },
    {
      id: 4,
      caption: 'Nice Mountains',
      date: 1660473384846,
      location: 'Saint Petersburg, Russia',
      imageUrl: 'https://cdn.quasar.dev/img/mountains.jpg'
    },
  ])

  const niceDate = (timeStamp) => {
    return date.formatDate(timeStamp, 'MMMM D hh:mm')
  }

</script>

<style lang="scss">
  .card-post {
    .q-img {
      min-height: 200px;
    }
  }
</style>
