<template>
  <div class="yyn-select">
    <div class="yyn-selected-tags-wrap" ref="yynTagsWrap">
      <div class="yyn-selected-tags" v-if="isMultiple">
          <span style="display: contents">
            <span
                v-for="tag in selectedTags"
                :key="keyProp ? tag[keyProp] : tag"
                class="yyn-tag"
            >
              {{labelProp ? tag[labelProp] : tag}}
            </span>
          </span>
      </div>
      <input
          v-model="selectedOption"
          class="yyn-placeholder"
          :placeholder="placeHolder"
          @click="optionsIsVisible = true"
          ref="yynInput"
          :readonly="!isFilterable"
      >
    </div>
    <div v-show="optionsIsVisible" class="yyn-options" ref="yynOptions" style="top: 28px;">
      <p
          v-for="item in filteredSelectedItems"
          :key="keyProp ? item[keyProp] : item"
          @click="selectOption(item)"
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
    selectedOption: null,
    optionsIsVisible: false,
    selectedTags: []
  }),
  computed: {
    filteredSelectedItems() {
      return this.items.filter(item => {
        return !this.selectedTags.includes(item)
      })
    }
  },
  methods: {
    selectOption(option) {
      if (this.isMultiple) {
        if (!this.selectedTags.includes(option)) {
          this.selectedTags.push(option)
          this.$nextTick(()=> {
            this.$refs.yynOptions.style.top = (parseInt(this.$refs.yynTagsWrap.offsetHeight) + 3) + 'px'
          })
          this.$emit('input', this.selectedTags)
        }
      } else {
        this.selectedOption = option[this.valueProp] ? option[this.valueProp] : option
        this.$emit('input', option[this.valueProp] ? option[this.valueProp] : option)
        this.optionsIsVisible = false
      }
    }
  }
}
</script>

<style lang="scss" scoped>
input {
  font-family: inherit;
  font-size: inherit;
  font-weight: 400;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 0px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
input:focus {
  color: #212529;
  background-color: #fff;
  border-color: #bdbdbd;
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(158, 158, 158, 0.25);
}
.yyn-select {
  position: relative;
  width: 220px;
}
.yyn-placeholder {
  display: block;
  margin: 0;
  padding: 3px;
  width: -webkit-fill-available;
}
.yyn-options {
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  width: fit-content;
  position: absolute;
  right: 0;
  min-width: 220px;
}
.yyn-options p {
  margin: 0;
  padding: 3px;
  border-bottom: 1px solid #bdbdbd;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-align: left;

  &:last-child {
    border-bottom: unset;
  }
}
.yyn-options p:hover {
  background-color: #409eff;
  cursor: pointer;
}
.yyn-selected-tags {
  position: relative;
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap
}
.yyn-selected-tags-wrap {
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
</style>
