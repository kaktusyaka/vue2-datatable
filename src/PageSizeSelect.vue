<template>
  <label name="PageSizeSelect">
    <select class="mt-1 form-select block w-full pl-3 pr-10 py-2 text-base leading-6 border-gray-300 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 sm:text-sm sm:leading-5 -page-size-select" v-model="query.limit"
      @change="query.offset = 0 /* reset to the first page */">
      <option v-for="i in pageSizeOptions" :value="i">{{ i }}</option>
    </select>
    {{ $i18nForDatatable('items / page') }}
  </label>
</template>
<script>
export default {
  name: 'PageSizeSelect',
  props: {
    query: { type: Object, required: true },
    pageSizeOptions: { type: Array, required: true }
  }
}
</script>
<style>
.-page-size-select {
  display: inline-block;
  width: 65px;
}
</style>
