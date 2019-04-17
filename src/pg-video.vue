<template>
  <div class="paragraph paragraph--video">
    <div
      v-if="$slots.title"
      class="title"
    >
      <slot name="title" />
    </div>
    <div
      v-if="!showThumbnail"
      ref="video"
      class="video"
    >
      <slot
        v-if="!autoplay"
        name="video"
      />
      <div
        v-if="autoplay"
        id="player"
        :style="{width: videoWidth, height: videoHeight}"
      />
    </div>
    <div
      v-if="showThumbnail"
      class="thumbnail"
      @click="loadVideo"
    >
      <slot name="thumbnail" />
      <div class="play-button" />
    </div>
  </div>
</template>
<script>
export default {
  name: 'PgVideo',
  data () {
    return {
      showThumbnail: false,
      autoplay: false,
      youtubeVideoId: false,
      videoLoaded: false,
      player: false,
      videoHeight: '360',
      videoWidth: '640'
    }
  },
  computed: {
    slotThumbnail () {
      return !!this.$slots.thumbnail
    }
  },
  mounted () {
    if (this.slotThumbnail) {
      this.showThumbnail = true
    }
    this.setYoutubeVideoData()
  },
  methods: {
    loadVideo () {
      this.showThumbnail = false
      this.autoplay = true
      this.renderYoutubeVideo()
    },
    setYoutubeVideoData () {
      let iframe = false
      let url = false
      if (this.$refs.video && this.$refs.video.children[0].children[0]) {
        iframe = this.$refs.video.children[0].children[0]
      }
      if (this.$refs.default && this.$refs.default.children[0].children[0]) {
        iframe = this.$refs.default.children[0].children[0]
      }

      url = iframe.src ? iframe.src : false
      this.videoWidth = iframe.width ? iframe.width : false
      this.videoHeight = iframe.height ? iframe.height : false

      if (url) {
        const matches = url.match(/(embed\/)(.{11})/)
        this.youtubeVideoId = matches[2]
      }
    },
    renderYoutubeVideo () {
      if (this.youtubeVideoId && !this.videoLoaded) {
        const tag = document.createElement('script')
        tag.src = 'https://www.youtube.com/iframe_api'
        tag.onload = this.createYoutubePlayer
        var firstScriptTag = document.getElementsByTagName('script')[0]
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag)
      }
    },
    createYoutubePlayer () {
      // We need to poll for the youtube ifram API to be ready.
      let x = 0
      let intervalId = window.setInterval(() => {
        x++
        if (typeof YT !== 'undefined') {
          // eslint-disable-next-line no-undef
          this.player = new YT.Player('player', {
            height: this.videoHeight,
            width: this.videoWidth,
            videoId: this.youtubeVideoId,
            events: {
              'onReady': function onPlayerReady (event) {
                event.target.playVideo()
              }
            }
          })
          window.clearInterval(intervalId)
        }
        if (x > 5) {
          window.clearInterval(intervalId)
        }
      }, 100)
    }
  }
}
</script>
