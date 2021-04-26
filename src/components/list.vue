<template>
  <div>
    리스트
  </div>
</template>

<script>
export default {
  props: ['carInfoList'],
  created() {
    console.log('list', this.carInfoList);
  },
};
</script>

<style>

</style>
