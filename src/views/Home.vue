<template>
  <div>
    <!-- nav start -->
    <div id="nav">
      <div class="list_btn">
        <span class="material-icons-outlined">format_list_bulleted</span>
      </div>
      <div class="line"></div>
      <div class="map_btn">
        <span class="material-icons-outlined">location_on</span>
      </div>
    </div>
    <!-- nav end -->
    <component
      :is="isShow.type"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import kakaoMap from '@/components/map.vue';

export default {
  name: 'Home',
  components: {
    kakaoMap,
  },
  data() {
    return {
      isShow: {
        type: 'kakaoMap',
      },
    };
  },
};
</script>

<style lang="scss" scoped>

#nav {
  background-color: #f2f2f2;
  width: 60px;
  padding: 5px 10px;
  display: flex;
  border-radius: 10px;
  border: 1px solid #ccc;
  .line {
    width: 1px;
    height: 100%;
    background-color: #fff;
  }

  // a {
  //   font-weight: bold;
  //   color: #2c3e50;

  //   &.router-link-exact-active {
  //     color: #42b983;
  //   }
  // }
}
</style>
