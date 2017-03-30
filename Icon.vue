<template>
  <svg version="1.1" :class="[clazz,'icon-' + name]" :width="w":height="h" :viewBox="box">
    <path :d="path.d" :fill="path.fill" :stroke="path.stroke" v-for="path in icon.paths"/>
  </svg>
</template>

<script>
  const convert = require('./lib/parse');
  export default {
    props: {
      name: {
        type: String,
        required: true
      },
      w: [Number, String],
      h: [Number, String]
    },
    computed: {
      clazz() {
        return {
          'svg-icon': true
        }
      },
      icon() {
        let xml = require(`!xml-loader!../../src/assets/svg/${this.name}.svg`);
        const t = xml.svg.$.viewBox.split(' ');
        // console.info(`src/svg/${this.name}.svg has been loaded`);
        return {
          width: t[2],
          height: t[3],
          paths: convert.SVGtoArray(xml.svg)
        }
      },
      box() {
        return `0 0 ${this.icon.width} ${this.icon.height}`
      }
    },
    register: function () {
      console.warn("inject deprecated since v1.2.0, SVG files can be loaded directly, so just delete the inject line.")
    },
  }
</script>
<style scoped>
  .svg-icon{
    display: inline-block;
    vertical-align: middle;
    fill: currentColor;
  }
</style>
