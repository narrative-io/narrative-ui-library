@@ -1,508 +0,0 @@
<template lang="pug">
  div
    h1 Number
    NioFilterGroup(:filters="filters")
      
</template>

<script>

import NioFilterGroup from '@/components/filter/FilterGroup'
import NioFilter from '@/components/filter/Filter'
import Default from './instances/Default'
import Range from './instances/Range'
import Currency from './instances/Currency'
import CustomText from './instances/CustomText'

export default {
  components: {
    NioFilterGroup,
    NioFilter
  },
  data: () => ({
    activeFilterName: null,
    filters: [
      Default,
      Range,
      Currency,
      CustomText
    ]
  }),
  mounted() {
   this.activeFilterName = this.filters[0].name
  },
  methods: {
    
  }
};
</script>

<style lang="sass" scoped>
.test-filters
 
</style>