<template>
  <div class="paragraph paragraph--video">
    <div
      v-if="$slots.title"
      class="title"
    >
      <slot name="title"/>
    </div>
    <div
      v-if="!showThumbnail"
      class="video"
    >
      <slot name="video" />
    </div>
    <div
      v-if="showThumbnail"
      @click="loadVideo"
      class="thumbnail"
    >
      <slot name="thumbnail"/>
      <div class="play-button"></div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'PgVideo',
  data () {
    return {
      showThumbnail: false
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
  },
  methods: {
    loadVideo () {
      this.showThumbnail = false
      // Todo: make autoplay work.
    }
  }
}
</script>
