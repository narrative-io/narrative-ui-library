<template lang="pug">
    v-checkbox.nio-checkbox(
      v-if="Array.isArray(this.model)"
      @change="updateModel($event)"
      :model="model" 
      :rules="parsedRules"
      v-bind="$attrs"
      v-on="$listeners" 
      ref="nio-checkbox-ref"
      :value="value"
      :input-value="this.model.find(val => val === this.value)"
    )
      template(v-for="(index, name) in $scopedSlots" v-slot:[name]="data")
        slot(:name="name" v-bind="data")  
      slot
    v-checkbox.nio-checkbox(
      v-else
      @change="$emit('update', $event)"
      :model="model" 
      :rules="parsedRules"
      v-bind="$attrs"
      v-on="$listeners" 
      ref="nio-checkbox-ref"
      :input-value="model"
    )  
      template(v-for="(index, name) in $scopedSlots" v-slot:[name]="data")
        slot(:name="name" v-bind="data")  
      slot   
</template>

<script>
  export default {
    name: 'nio-checkbox',
    props: {
      "model": { required: false },
      "rules": { required: false },
      "value": { required: false}
    },
    model: {
      prop: "model",
      event: "update"
    },
    data: () => ({
      parsedRules: []
    }),
    methods: {
      updateModel(state) {
        if (Array.isArray(this.model)) {
          if (state === null) {
            this.$emit('update', this.model.filter(val => val !== this.value))
          } else {
            this.model.push(state)
            this.$emit('update', this.model)
          }
        } else {
          this.$emit('update', this.state === true ? true : false)
        }
      },
      parseRules() {
        if (this.rules) {
          this.rules.map((rule, index) => {
            let func = rule.toString()
            let funcBody = func.slice(func.indexOf("{") + 1, func.lastIndexOf("}"))
            this.parsedRules[index] = new Function("value", funcBody)
          });
        }
      }
    },
    mounted() {	
      this.$emit('mounted')
    },
    destroyed() {
      this.$emit('destroyed')
    }
  }
</script>

<style lang="sass" scoped>
  @import '../styles/mixins/_checkbox'  
</style>
