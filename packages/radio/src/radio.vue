<template>
  <div class="mint-radiolist">
    <label class="mint-radiolist-title" v-text="title"></label>
    <x-cell v-for="option in options">
      <div slot="title">
        <label>
          <span
            :class="{'is-right': align === 'right'}"
            class="mint-radio">
            <input
              class="mint-radio-core"
              type="radio"
              v-model="value"
              :disabled="option.disabled"
              :value="option.value || option">
          </span>
          <span class="mint-radio-label" v-text="option.label || option"></span>
        </label>
      </div>
    </x-cell>
  </div>
</template>

<script>
import XCell from 'packages/cell/index.js';
import 'packages/cell/style.css';

/**
 * mt-radio
 * @module components/radio
 * @desc 单选框列表，依赖 cell 组件
 *
 * @param {string[], object[]} options - 选项数组，可以传入 [{label: 'label', value: 'value', disabled: true}] 或者 ['ab', 'cd', 'ef']
 * @param {string} value - 选中值
 * @param {string} title - 标题
 * @param {string} [align=left] - checkbox 对齐位置，`left`, `right`
 *
 * @example
 * <mt-radio :value.sync="value" :options="['a', 'b', 'c']"></mt-radio>
 */
export default {
  name: 'mt-radio',

  props: {
    title: String,
    align: String,
    options: {
      type: Array,
      required: true
    },
    value: String
  },

  components: {
    XCell
  }
};
</script>

<style lang="css">
  @import "../../../src/style/var.css";

  @component-namespace mint {
    @component radiolist {

      .mint-cell {
        padding: 0;
      }

      .mint-cell-title {
        padding: 16px 10px;
      }

      @descendent title {
        font-size: 12px;
        margin: 8px;
        display: block;
        color: $radio-title-color;
      }
    }

    @component radio {
      @when right {
        float: right;
      }

      @descendent label {
        vertical-align: middle;
        margin-left: 6px;
      }

      @descendent core {
        appearance: none;
        outline: 0;
        background-color: $color-white;
        border-radius: 100%;
        border: 1px solid #ccc;
        position: relative;
        size: 20px;
        vertical-align: middle;

        &::after {
          content: " ";
          border-radius: 100%;
          position: absolute 5px * * 5px;
          size: 8px;
        }

        &:checked {
          background-color: $color-blue;
          border-color: $color-blue;

          &::after {
            background-color: $color-white;
          }
        }

        &[disabled] {
          background-color: $color-grey;
          border-color: #ccc;
        }
      }
    }
  }
</style>
