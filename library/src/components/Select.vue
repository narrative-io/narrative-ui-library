<template lang="pug">
  v-select.nio-select(
    :items="items"
    :class="{ small: smallAttr, 'hide-selections': hideSelections, 'selection-pills': selectionPills }"
    :solo="smallAttr"
    :model="model"
    :menu-props="{contentClass: 'nio-select-menu', offsetY: true, nudgeBottom: 10  }"
    outlined
    :attach="attach ? node : undefined"
    v-bind="$attrs"
    v-on="$listeners"
    @input="updateModel($event)"
    ref="nio-select-ref"
    :value="value"
    :item-value="valueKey"
    :item-text="textKey"
  )
    template(v-for="(index, name) in $scopedSlots" v-slot:[name]="data")
      slot(:name="name" v-bind="data")
    template(v-slot:append)
      svg(style="width:24px;height:24px" viewBox="0 0 24 24")
        path(fill="#425290" d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z")
    template(v-slot:selection="{ item, index }" v-if="hideSelections")
      span(v-if="index === 0") {{ labelText }}
    template(v-slot:selection="{ item, index }" v-if="selectionPills && !hideSelections")
      NioPill(
        :text="textKey ? item[textKey] : item"
        selected-value
      )
</template>


<script>
import { text } from '../plugins/fontawesome-svg-core'

import NioPill from './Pill'

export default {
  name: 'nio-select',
  props: {
    "model": { required: false },
    "rules": { required: false },
    "items": { required: true }
  },
  model: {
    prop: "model",
    event: "update"
  },
  data: () => ({
    node: null,
    smallAttr: false,
    attach: false,
    hideSelections: false,
    selectionPills: false,
    labelText: null,
    textKey: null,
		valueKey: null,
		value: null
  }),
  methods: {
    applyKeys() {
      const attributes = this.$el.attributes
      const textKey = attributes.getNamedItem('item-text') ? attributes.getNamedItem('item-text').value : undefined
      const valueKey = attributes.getNamedItem('item-value') ? attributes.getNamedItem('item-value').value : undefined
      if (this.items && this.items.length > 0) {
        if (!this.items[0].length && textKey) {
          this.textKey = textKey
        } else {
          this.textKey = undefined
        }
         if (!this.items[0].length && valueKey) {
          this.valueKey = valueKey
        } else {
          this.valueKey = undefined
        }
      } else {
        this.textKey = undefined
        this.valueKey = undefined
      }
    },
    applyHelperAttributes() {
      const attributes = this.$el.attributes
      if (attributes.getNamedItem('small')) {
        this.smallAttr = true
      }
      if (attributes.getNamedItem('attach-to-parent')) {
        this.attach = true
      }
      if (attributes.getNamedItem('hide-selections')) {
        this.hideSelections = true
      }
      if (attributes.getNamedItem('label')) {
        this.labelText = attributes.getNamedItem('label').value
      }
      if (attributes.getNamedItem('selection-pills')) {
        this.selectionPills = true
      }
		},
		updateModel(event) {
			this.$emit('update', event)
		}
  },
  mounted() {	
    this.applyHelperAttributes()
		this.applyKeys()
		this.updateModel(this.model)
		this.value = this.model
    this.$emit('mounted')
    this.node = this.$refs['nio-select-ref'].$vnode.elm
  },
  destroyed() {
    this.$emit('destroyed')
  },
  watch: {
    items(val) {
      this.applyKeys()
    }
  },
  components: { NioPill }
}
</script>

<style lang="sass">
  @import '../styles/mixins/_menu'
  
  .v-menu__content.nio-select-menu
    +nio-menu
</style>

<style lang="sass" scoped>
  @import '../styles/mixins/_select'  
</style>

