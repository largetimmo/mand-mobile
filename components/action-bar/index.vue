<template>
  <div
    class="md-action-bar"
    :class="{'with-text': hasText, 'multi-action': !!this.actions.length }">
    <div class="md-action-bar-text" v-if="hasText">
      <slot></slot>
    </div>
    <div class="md-action-bar-button">
      <template v-for="(item, index) in actions">
        <div
          class="button-item"
          :key="index"
          :class="{disabled: !!item.disabled,'button-active':item.isActive}"
          @click="$_onBtnClick($event, item)"
          v-html="item.text"
        ></div>
      </template>
    </div>
  </div>
</template>

<script>import {isEmptyObject} from '../_util'

export default {
  name: 'md-action-bar',

  props: {
    actions: {
      type: Array,
      default: [],
    },
    hasText: {
      type: Boolean,
      default() {
        return !isEmptyObject(this.$slots)
      },
    },
  },

  methods: {
    // MARK: events handler
    $_onBtnClick(event, action) {
      if (action.disabled) {
        return
      }
      action.onClick && action.onClick(event, action)
      this.$emit('click', event, action)
    },
  },
}
</script>

<style lang="stylus">
.md-action-bar
  position fixed
  z-index action-bar-zindex
  left 0
  bottom 0
  width action-bar-width
  height action-bar-height
  padding-bottom constant(safe-area-inset-bottom)
  background color-bg-base
  clearfix()
  .md-action-bar-text
    float left
    display flex
    height 100%
    width 65%
    padding-left action-bar-text-left
    align-items center
    overflow hidden
    color action-bar-text-color
    font-size action-bar-text-font-size
    box-sizing border-box
  .md-action-bar-button
    display flex
    height 100%
    .button-item
      display flex
      float right
      align-items center
      justify-content center
      flex 1
      color action-bar-button-color
      font-size action-bar-button-font-size
      font-weight action-bar-button-font-weight
      background action-bar-button-fill
      hairline(right, color-border-base)
      -webkit-user-select none
      -webkit-tap-highlight-color transparent
      &.disabled
        opacity action-bar-button-disabled-opacity
      .button-active
        background action-bar-button-fill-highlight
        color action-bar-button-color-highlight
        &.disabled
          background action-bar-button-disabled-bg
          color action-bar-button-disabled-color
        &::before
          display none
      &::after
        absolute-pos()
        display none
        content ''
        position absolute
        box-sizing border-box
        background-color action-bar-button-tap-bg
      &:active::after
        display block

  &.with-text.multi-action
    .md-action-bar-text
      width 40%
</style>
