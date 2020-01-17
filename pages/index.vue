<template>
  <div class="container">
    <div>
      <h1 class="title">nuxt-shaka-player</h1>
      <video
        id="video"
        width="640"
        poster="//shaka-player-demo.appspot.com/assets/poster.jpg"
        controls
        autoplay
      ></video>
    </div>
  </div>
</template>

<script>
import shaka from 'shaka-player'

export default {
  name: 'Top',
  computed: {
    manifest() {
      return 'https://storage.googleapis.com/shaka-demo-assets/angel-one/dash.mpd'
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      const video = document.getElementById('video')
      const player = new shaka.Player(video)
      window.player = player
      player.addEventListener('error', this.onError)

      player
        .load(this.manifest)
        .then(function() {
          // This runs if the asynchronous load is successful.
          console.log('The video has now been loaded!')
        })
        .catch(this.onError)
    },
    onError(e) {
      console.log('error', e)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
