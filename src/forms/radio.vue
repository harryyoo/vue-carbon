<template>
  <label class="vc-radio" :class="{'label-left': labelLeft}">
    <input type="radio" :name="name" :value="value" v-model="model">
    <div class="vc-radio-label" v-if="label && labelLeft">{{label}}</div>
    <div class="vc-radio-icon"></div>
    <div class="vc-radio-label" v-if="label && !labelLeft">{{label}}</div>
  </label>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: '',
      required: true
    },
    value: {
      type: String,
      default: ''
    },
    model: {
      type: String,
      required: true,
      default: ''
    },
    label: {
      type: String,
      default: ''
    },
    labelLeft: {
      type: Boolean,
      default: false
    }
  },
  watch: {
    value () {
      this.$emit('input-change', this.model)
    }
  }
}
</script>

<style lang="less">
@import "../utils/_vars.less";
@import "../utils/_mixins.less";
.vc-radio {
  position: relative;
  display: inline-block;;
  height: 36px;
  line-height: 36px;
  margin-right: 32px;
  input[type="radio"] {
    display: none;
    &:checked{
      + .vc-radio-icon,
      + .vc-radio-label + .vc-radio-icon{
        border-color: @red;
        &:after{
          transform: scale(1);
        }
      }
    }
  }
  * {
    pointer-events: none;
  }
  &.label-left{

    .vc-radio-label {
      margin-left: 0;
      margin-right: 8px;
    }
  }

  &:last-child{
    margin-right: 0;
  }
}

.vc-radio-icon {
  width: 20px;
  height: 20px;
  border-radius: 36px;
  border-width: 2px;
  border-style: solid;
  border-color: @body_color;
  background: transparent;
  transition-duration: 300ms;
  position: relative;
  &:after {
    content:' ';
    display: block;
    width: 10px;
    height: 10px;
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -5px;
    margin-top: -5px;
    background-color: @red;
    border-radius: 100%;
    transform: scale(0);
    transition-duration: 300ms;
  }
}

.vc-radio-label{
  color: @color;
  font-size: 16px;
  margin-left: 8px;
  margin-right: auto;
}

.vc-radio-label,
.vc-radio-icon {
  display: inline-block;
  vertical-align: middle;
}
</style>
