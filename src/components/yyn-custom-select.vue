<template>
  <div class="yyn-select">
    <input
        class="yyn-placeholder"
        :placeholder="placeHolder"
        @click="optionsIsVisible = true"
        ref="yynInput"
        :readonly="!isFilterable"
    >
    <div v-show="optionsIsVisible" class="yyn-options" ref="yynOptions" style="top: 28px;">
      <p
          v-for="item in items"
          :key="keyProp ? item[keyProp] : item"
          class="yyn-item"
      >
        {{labelProp ? item[labelProp] : item}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'YynCustomSelect',
  props: {
    placeHolder: {
      type: String,
      default() {
        return 'Select'
      }
    },
    items: {
      type: Array,
      default() {
        return []
      }
    },
    isMultiple: {
      type: Boolean,
      default() {
        return false;
      }
    },
    isFilterable: {
      type: Boolean,
      default() {
        return false;
      }
    },
    labelProp: {
      type: String,
      default() {
        return null
      }
    },
    valueProp: {
      type: String,
      default() {
        return null
      }
    },
    keyProp: {
      type: String,
      default() {
        return null
      }
    }
  },
  data: () => ({
    optionsIsVisible: false,
  }),
  methods: {}
}
</script>

<style scoped>

</style>
