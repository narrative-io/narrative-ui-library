<template lang="pug">
  .nio-filter-properties.string-many
    NioFilterProperty(
      :description="description"
      :options="filter.options ? filter.options : defaultOptions"
      v-bind:value.sync="filter.value"
    )
      template(v-slot:custom-option)
        .string-many-custom
          .manual-entry-only(
            v-if="filter.customOption.config.manualEntryOnly"
          )
            NioRadioGroup(
              v-if="filter.customOption.value.listType"
              v-model="filter.customOption.value.listType"
            )
              NioRadioButton(value="include" label="Include")
              NioRadioButton(value="exclude" label="Exclude")
            NioTextarea(
              v-model="filter.customOption.value.manualEntry"
            )
          NioTabs(
            :tabs="tabs"
            v-model="activeTab"
            v-else
          )
            template(v-slot:list)
              NioSlatTable(
                v-if="filter.customOption.config.list.items.length > 0 && filter.customOption.config.list.columns.length > 0 && filter.customOption.config.list.searchableProps"
                multi-select		
                search-header
                dense-rows				
                :items="filter.customOption.config.list.items"
                :columns="filter.customOption.config.list.columns"
                :defaultSelection="initialListItems"
                :searchableProps="filter.customOption.config.list.searchableProps"
                pagination
                @selectionChanged="listSelectionChanged($event)"
              )
                template(v-slot:custom-header-element)
                  NioRadioGroup(
                    v-model="filter.customOption.value.listType"
                    v-if="filter.customOption.value.listType"
                  )
                    NioRadioButton(value="include" label="Include")
                    NioRadioButton(value="exclude" label="Exclude")
            template(v-slot:manual)
              NioRadioGroup(
                v-if="filter.customOption.value.listType"
                v-model="filter.customOption.value.listType"
              )
                NioRadioButton(value="include" label="Include")
                NioRadioButton(value="exclude" label="Exclude")
              NioTextarea(
                v-model="filter.customOption.value.manualEntry"
              )
</template>

<script>

import NioFilterProperty from '../FilterProperty'
import NioTabs from '../../Tabs'
import NioSlatTable from '../../table/SlatTable'
import NioRadioGroup from '../../RadioGroup'
import NioRadioButton from '../../RadioButton'
import NioTextarea from '../../Textarea'

export default {
  name: 'nio-filter-properties-string-many',
  props: {
    "filter": { type: Object, required: true },
  },
  data: () => ({
    initialListItems: [],
    description: 'Select the data to include',
    tabs: [
      {
        name: 'list',
        label: 'Select from list'
      },
      {
        name: 'manual',
        label: 'Manual entry'
      }
    ],
    activeTab: 'list'
  }),	
  computed: {
    defaultOptions() {
      if (!this.filter) {
        return []
      }
      return [
        {
          label: `All ${this.filter.name}s`,
          value: 'default'
        },
        {
          label: "Include if present",
          value: 'ifPresent'
        },
        {
          label: 'Custom',
          value: 'custom'
        }
      ]
    }
  },
  mounted() {
    if (!this.filter.customOption.config.manualEntryOnly) {
      this.initialListItems = this.filter.customOption.value.items.length ? this.filter.customOption.value.items.map(item => item.id) : []
    }
    this.updateValue()
  },
  methods: {
    listSelectionChanged(val) {
      this.filter.customOption.value.items = val
    },
    updateValue() {
      const options = this.filter.options ? this.filter.options : this.defaultOptions
      this.$emit('valueChanged', [options.find(option => option.value === this.filter.value).label])
    }
  },
  watch: {
    filter: {
      deep: true,
      handler() {
        this.updateValue()
      }
    }
  },
  components: { NioFilterProperty, NioTabs, NioSlatTable, NioRadioGroup, NioRadioButton, NioTextarea }
}
</script>

<style lang="sass" scoped>
</style>