<template>
  <div id="app" :style="{ display: 'flex', textAlign: 'center' }">
    <!--<div>
      <ColorPicker
          :color="color"
          :onStartChange="color => onChange(color, 'start')"
          :onChange="color => onChange(color, 'change')"
          :onEndChange="color => onChange(color, 'end')"
      />
    </div>-->
    <div>
        <!--:gradien="gradient"-->
        <ColorPicker
          :color="color"
          :gradient="gradient"
          :is-gradient="isShowGradient"
          :onChange="color => onChange(color, 'change')"
          :onEndChange="color => onChange(color, 'end')"
      />
    </div>
  </div>
</template>

<script>
import { ColorPicker } from './lib'

export default {
  name: 'App',
  components: {
    ColorPicker
  },

  data() {
    return {
      color: {
        red: 255,
        green: 0,
        blue: 0,
        alpha: 1,
      },
      isShowGradient: false,
      gradient: {
        type: 'solid',
        degree: 0,
        points: [
          {
            left: 0,
            red: 255,
            green: 255,
            blue: 255,
            alpha: 1,
          },
          {
            left: 100,
            red: 255,
            green: 0,
            blue: 0,
            alpha: 1,
          },
        ],
      }
    };
  },
  methods: {
    onChange(attrs,type) {
      console.log(attrs,type)
      if (!attrs.type){
        this.gradient = {
          type: 'solid',
          degree: 0,
          points: [
            {
              left: 0,
              red: 255,
              green: 255,
              blue: 255,
              alpha: 1,
            },
            {
              left: 100,
              red: attrs.red?attrs.red:255,
              green: attrs.green?attrs.green:0,
              blue: attrs.blue?attrs.blue:0,
              alpha: attrs.alpha?attrs.alpha:1,
            },
          ],
        }
        this.isShowGradient = false;
        this.color = { ...attrs };
      }else {
        let str = attrs.style.split('rgba')
        let a =str[2].slice(1,-7).split(',')
        this.color = {
          red: Number(a[0]),
          green: Number(a[1]),
          blue: Number(a[2]),
          alpha: Number(a[3]),
        };
        this.isShowGradient = attrs.type != 'solid';
      }
    }
  }
}
</script>

<style src="@/lib/index.scss" lang="scss" />
