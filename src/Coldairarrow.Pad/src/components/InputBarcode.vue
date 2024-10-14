<template>
  <div>
    <a-input v-model="curValue" @change="handlerInputChange" v-bind="$attrs">
      <a-icon slot="addonAfter" type="scan" @click="$refs.barcodeReader.openReader()"></a-icon>
    </a-input>
    <barcode-reader ref="barcodeReader" @success="handlerReaderDone"></barcode-reader>
  </div>
</template>

<script>
import BarcodeReader from './BarcodeReader'
export default {
  inheritAttrs: false,
  components: {
    BarcodeReader
  },
  props: {
    value: { type: String, required: false, default: '' }
  },
  data() {
    return {
      curValue: ''
    }
  },
  watch: {
    value(value) {
      this.curValue = value
    }
  },
  methods: {
    handlerInputChange() {
      this.$emit('input', this.curValue)
    },
    handlerReaderDone(result) {
      this.curValue = result
      this.$emit('input', result)
    }
  }
}
</script>

<style>
</style>