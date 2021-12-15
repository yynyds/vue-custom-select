<template>
  <el-select
      v-model="selected"
      placeholder="Select"
      clearable
      @change="onChange">
    <el-option
        v-for="item in items"
        :key="item.id"
        :label="item.title"
        :value="item.id">
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
