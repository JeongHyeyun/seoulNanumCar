<template>
  <div id="wrap">
    <!-- nav start -->
    <div id="nav">
      <!-- list_btn -->
      <div @click="isShow.type = 'locationLists'" class="list_btn"
          :class="{'clicked clicked-list' : isShow.type === 'locationLists'}">
        <span class="material-icons">list</span>
      </div>
      <div class="line"></div>
      <!-- map_btn -->
      <div @click="isShow.type = 'locationMap'" class="map_btn"
          :class="{'clicked clicked-map' : isShow.type === 'locationMap'}">
        <span class="material-icons">location_on</span>
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
import locationMap from '@/components/map.vue';
import locationLists from '@/components/list.vue';

export default {
  name: 'Home',
  components: {
    locationMap,
    locationLists,
  },
  data() {
    return {
      isShow: {
        type: 'locationMap',
      },
    };
  },
};
</script>

<style lang="scss" scoped>
#wrap {
  // ******************************************** nav
  #nav {
    background-color: #f2f2f2;
    width: 90px;
    display: flex;
    border-radius: 10px;
    border: 1px solid #ccc;
    margin-left: auto;
    .list_btn, .map_btn {
      padding: 3px 10px;
      font-size: 12px;
      cursor: pointer;
      color: #ccc;
    }
    .line {
      width: 1px;
      height: auto;
      background-color: #fff;
    }
    // ******************************************** clicked
    .clicked {
      background-color: #fff;
      color: #666;
      &-list {
        border-top-left-radius: 10px;
        border-bottom-left-radius: 10px;
      }
      &-map {
        border-top-right-radius: 10px;
        border-bottom-right-radius: 10px;
      }
    }
  }
}
</style>
