<template>
  <span v-if="false" />
</template>

<script>
// Test on: https://cards-dev.twitter.com/validator
// Test on: https://developers.facebook.com/tools/debug/
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    image: {
      type: String,
      default: ''
    }
  },
  head () {
    let ogImage = ''
    if (this.$route.path === '/') {
      ogImage = 'https://autotube.app/card.png'
    } else if (this.image === '') {
      const title = Buffer.from(this.title).toString('base64')
      const footer = Buffer.from('https://autotube.app' + this.$route.fullPath).toString('base64')
      ogImage = `https://og-img.ld83.com/img/${title}/${footer}?tpl=att`
    } else {
      ogImage = this.image
    }

    return {
      meta: [
        {
          hid: 'twitter:card',
          name: 'twitter:card',
          content: 'summary_large_image'
        },
        {
          hid: 'twitter:title',
          name: 'twitter:title',
          content: this.title
        },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.description
        },
        {
          hid: 'twitter:image',
          name: 'twitter:image',
          content: ogImage
        },
        {
          hid: 'twitter:image:alt',
          name: 'twitter:image:alt',
          content: this.title
        },
        {
          hid: 'og:title',
          property: 'og:title',
          content: this.title
        },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.description
        },
        {
          hid: 'og:image',
          property: 'og:image',
          content: ogImage
        },
        {
          hid: 'og:image:secure_url',
          property: 'og:image:secure_url',
          content: ogImage
        },
        {
          hid: 'og:image:alt',
          property: 'og:image:alt',
          content: this.title
        }
      ]
    }
  }
}
</script>
