<template>
  <div class="paragraph paragraph--video">
    <div
      v-if="$slots.title"
      class="title"
    >
      <slot name="title"/>
    </div>
    <div class="video">
      <slot :name="$slots.video ? 'video': 'default'" />
    <div>
    <div
      v-if="$slots.thumbnail"
      class="thumbnail"
    >
      <slot name="thumbnail"/>
    </div>
  </div>
</template>
<script>
export default {
  name: 'PgVideo'
}
</script>
