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
            <i class="el-icon-error yyn-close-icon-tag" @click="removeFromSelectedTagsList(tag)"></i>
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
      <i class="el-icon-error yyn-close-icon" v-if="!isMultiple && selectedOption" @click="selectedOption = '', $emit('input', '')"></i>
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
    selectedTags: [],
    localItems: []
  }),
  computed: {
    filteredSelectedItems: {
      get() {
        return this.localItems.filter(item => {
          return !this.selectedTags.includes(item)
        })
      },
      set(newValue) {
        this.localItems = newValue
      }
    }
  },
  watch: {
    selectedOption(value) {
      if (value && this.isFilterable) {
        this.localItems = this.items.filter(item => {
          if (this.labelProp) {
            return item[this.labelProp].includes(value)
          } else {
            return item.includes(value)
          }
        })
      } else {
        this.localItems = this.items
      }
    }
  },
  methods: {
    selectOption(option) {
      if (this.isMultiple) {
        if (!this.selectedTags.includes(option)) {
          this.selectedTags.push(option)
          this.$nextTick(()=> {
            this.changeOptionsTop()
            this.resetPlaceHolder('')
            this.selectedOption = null
            if (this.filteredSelectedItems.length === 0 && this.localItems.length === 4) {
              this.changeOptionsBorder('0px solid')
            }
          })
          this.$emit('input', this.selectedTags)
        }
      } else {
        this.selectedOption = option[this.labelProp] ? option[this.labelProp] : option
        this.$emit('input', option[this.labelProp] ? option[this.labelProp] : option)
        this.optionsIsVisible = false
      }
    },
    removeFromSelectedTagsList(tag) {
      this.selectedTags = this.selectedTags.filter(item => {
        if (this.keyProp) {
          return item[this.keyProp] !== tag[this.keyProp]
        } else {
          return item !== tag
        }
      })
      this.$emit('input', this.selectedTags)
      if (this.selectedTags.length === 0) {
        this.$nextTick(()=> { this.resetPlaceHolder(this.placeHolder) })
      }
      this.$nextTick(()=> {
        this.changeOptionsTop()
        this.changeOptionsBorder('1px solid #bdbdbd')
      })
    },
    resetPlaceHolder(value) {
      this.$refs.yynInput.placeholder = value
    },
    changeOptionsTop() {
      this.$refs.yynOptions.style.top = (parseInt(this.$refs.yynTagsWrap.offsetHeight) + 3) + 'px'
    },
    changeOptionsBorder(value) {
      this.$refs.yynOptions.style.border = value
    },
    closeOptions(e) {
      if (!e.target.classList.contains('yyn-close-icon-tag') &&
          !e.target.classList.contains('yyn-placeholder') &&
          !e.target.classList.contains('yyn-item') &&
          !e.target.classList.contains('yyn-tag')) {
        this.optionsIsVisible = false
      }
    }
  },
  beforeMount() {
    this.localItems = this.items
  },
  mounted() {
    document.addEventListener('click', this.closeOptions.bind(this), true)
  },
  beforeDestroy() {
    document.removeEventListener('click', this.closeOptions)
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
  padding: 3px 20px 3px 3px;
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
.yyn-tag {
  position: relative;
  background-color: #ecf5ff;
  border-color: #d9ecff;
  height: 32px;
  padding: 0 16px 0 10px;
  line-height: 30px;
  font-size: 12px;
  color: #409eff;
  border-width: 1px;
  border-style: solid;
  border-radius: 4px;
  box-sizing: border-box;
  white-space: nowrap;
  box-sizing: border-box;
  border-color: transparent;
  margin: 2px 0 2px 6px;
  max-width: 100%;

  .yyn-close-icon-tag {
    position: absolute;
    right: 0;
    top: 10px;
    color: #e56d6d;
    cursor: pointer;
  }
}
.yyn-close-icon {
  position: absolute;
  right: 2px;
  top: 6px;
  cursor: pointer;
}
.yyn-selected-tags-wrap {
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
</style>
