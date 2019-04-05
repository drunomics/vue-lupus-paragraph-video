# vue-lupus-paragraph-video
Vue video paragraph component.

## Install

via npm:
`npm install https://github.com/drunomics/vue-lupus-paragraph-video.git`


## Slots
You can use the following slots

- `title` ( optional )
  Title.
- `video` ( required )
  Video.
- `thumbnail` ( optional )
  Video thumbnail. Should be a <lupus-image>

## Example
```
<pg-video>
  <h1 slot="title">Video Title</h1>
  <div slot="video">
    <!-- embed code -->
  </div>
  <lupus-image
    slot="thumbnail"
    width="768"
    height="432"
    :src="..."
  />
</pg-video>
```
