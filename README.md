# vue-lupus-paragraph-video
Vue video paragraph component.

## Install

via npm:
`npm install https://github.com/drunomics/vue-lupus-paragraph-video.git`


## Slots
You can use the following slots

- `title` ( optional )
  Title.
- `video` ( default )
  Video.
- `thumbnail` ( optional )
  Video thumbnail.

## Example
```
<pg-image>
  <lupus-image
    width="200" height="300"
    :src="..."
    slot="image"
  >
    <img :src="...">
  </lupus-image>
  <span slot="copyright">Lorem Ipsum.</span>
  <span slot="caption">Lorem Ipsum.</span>
</pg-image>
```
