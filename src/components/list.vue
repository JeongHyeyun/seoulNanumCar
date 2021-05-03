<template>
  <div>
    리스트
  </div>
</template>

<script>
export default {
  props: ['covidCenter'],
  created() {
    console.log('list', this.covidCenter);
  },
};
</script>

<style>

</style>
