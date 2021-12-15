<template>
  <el-select
      v-model="selected"
      placeholder="Select"
      :multiple="isMultiple"
      :filterable="isFilterable"
      clearable
      @change="onChange">
    <el-option
        v-for="item in items"
        :key="keyProp ? item[keyProp] : item"
        :label="labelProp ? item[labelProp] : item"
        :value="valueProp ? item[valueProp] : item">
    </el-option>
  </el-select>
</template>

<script>
export default {
  name: 'CustomSelect',
  props: {
    items: {
      type: Array,
      default() {
        return [1, 2, 3]
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
    selected: null
  }),
  methods: {
    onChange() {
      this.$emit('input', this.selected);
    }
  }
}
</script>

<style scoped>

</style>
