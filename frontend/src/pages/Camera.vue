<template>
  <q-page
    class="constrain-more q-pa-md"
  >
    <div
      class="camera-frame q-pa-md"
    >
      <video
        v-show="!imageCaptured"
        ref="video"
        class="full-width"
        autoplay
      />
      <canvas
        v-show="imageCaptured"
        ref="canvas"
        class="full-width"
        height="240"
      />
    </div>

    <div
      class="text-center q-pa-md"
    >
      <q-btn
        v-if="hasCameraSupport"
        size="lg"
        round
        color="grey-10"
        icon="eva-camera"
        @click="captureImage"
      />
      <div
        v-else
        class="row justify-center q-ma-md"
      >
      <q-file
        dense
        @input="captureImageFallback"
        accept="image/*"
        class="col col-sm-6"
        label="Chose an Image"
        v-model="uploadedImage"
      >
        <template
          v-slot:prepend
        >
          <q-icon
            name="eva-attach-outline"
          />
        </template>
      </q-file>
      </div>

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
  import { ref, onMounted, onBeforeUnmount } from 'vue'
  import { uid } from 'quasar'

  const post = ref({
    id: uid(), // TODO поудмать над тем чтобы перенесть создание id на бэк
    caption: 'test caption',
    location: 'test location',
    photo: null,
    date: Date.now() // TODO поудмать над тем чтобы перенесть создание таймштампа на бэкэнде()
  })

  /*
    Handling Video
  */
  require('md-gum-polyfill') //либа нужна для корректного ображения к камера во всех браузерах
  const video = ref(null)
  const hasCameraSupport = ref(true)
  onMounted(() => { initCamera() })
  const initCamera = () => {
    navigator.mediaDevices.getUserMedia({
      video: true
    }).then(stream => {
      video.srcObject = stream
    }).catch(error => {
      hasCameraSupport.value = false
    })
  }

  /*
   Handling taking the picture
  */
  const canvas = ref(null)
  const imageCaptured = ref(false)
  const captureImage = () => {
    let v = video
    let c = canvas
    c.width = v.getBoundingClientReact.width
    c.height = v.getBoundingClientReact.height
    let context = canvas.getContext('2d')
    context.drawImage(video, 0, 0, c.width, c.height)
    imageCaptured.value = true
    post.value.photo = dataURItoBlob(c.toDataURL())
    disableCamera()
  }
  const dataURItoBlob = (dataURI) => {
    // convert base64 to raw binary data held in a string
    // doesn't handle URLEncoded DataURIs - see SO answer #6850276 for code that does this
    let byteString = atob(dataURI.split(',')[1])
    // separate out the mime component
    let mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0]
    // write the bytes of the string to an ArrayBuffer
    let ab = new ArrayBuffer(byteString.length)
    // create a view into the buffer
    let ia = new Uint8Array(ab)
    // set the bytes of the buffer to the correct values
    for (let i = 0; i < byteString.length; i++) {
      ia[i] = byteString.charCodeAt(i)
    }
    // write the ArrayBuffer to a blob, and you're done
    let blob = new Blob([ab], {type: mimeString})
    return blob
  }

  /*
   Handling upload image
   (when browser can't access camera for some reason)
  */
  const uploadedImage = ref([])
  const captureImageFallback = (file) => {
    post.value.photo = file

    let c = canvas
    let context = c.value.getContext('2d')

    let reader = new FileReader()
    reader.onload = event => {
      let img = new Image()
      img.onload = () => {
        canvas.value.width = img.width
        canvas.value.height = img.height
        context.drawImage(img,0,0)
        imageCaptured.value = true
      }
      img.src = event.target.result
    }
    reader.readAsDataURL(file) // todo fix - тет валится, что файл не Blob
  }

  /*
   Handling disable camera when living the page
  */
  onBeforeUnmount(() => { disableCamera() })
  // todo когда будет камера, убедиться что она отключается после создания снимка или после перехода на другую страницу!
  const disableCamera = () => { video.srcObject.getAudioTracks().forEach(track => { track.stop() }) }

</script>


<style lang="scss">
  .camera-frame {
    border: 2px solid $grey-10;
    border-radius: 10px;
  }
</style>
