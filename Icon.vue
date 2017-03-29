<template>
  <svg version="1.1" :class="[clazz, 'icon-' + name]" :role="label ? 'img' : 'presentation'" :aria-label="label" :width="w"
       :height="h" :viewBox="box">
    <path :d="path.d" :fill="path.fill" :stroke="path.stroke" v-for="path in icon.paths"/>
  </svg>
</template>

<style>
  .svg-icon {
    display: inline-block;
    fill: currentColor;
  }

  .svg-icon.flip-horizontal {
    transform: scale(-1, 1);
  }

  .svg-icon.flip-vertical {
    transform: scale(1, -1);
  }

  .svg-icon.spin {
    animation: fa-spin 1s 0s infinite linear;
  }

  @keyframes fa-spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>

<script>

  const convert = require('./lib/parse');

  export default {
    props: {
      name: {
        type: String,
        required: true
      },
      w: [Number, String],
      h: [Number, String],
      spin: Boolean,
      flip: {
        validator: function (val) {
          return val === 'horizontal' || val === 'vertical'
        }
      },
      label: String,
      index: String,
      currentIndex: String
    },
    computed: {
      clazz() {
        return {
          'svg-icon': true,
          spin: this.spin,
          'flip-horizontal': this.flip === 'horizontal',
          'flip-vertical': this.flip === 'vertical',
          active: this.index === this.currentIndex
        }
      },
      icon() {
        let xml = require(`!xml-loader!../../src/svg/${this.name}.svg`);
        const t = xml.svg.$.viewBox.split(' ');
        console.info(`src/svg/${this.name}.svg has been loaded`);
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
