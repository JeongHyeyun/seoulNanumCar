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
/* eslint-disable no-loop-func */
import locationMap from '@/components/map.vue';
import locationLists from '@/components/list.vue';
// import axios from 'axios';

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
      carInfoList: [],
    };
  },
  created() {
    // let startNumber = 1;
    // let endNumber = 1000;
    // let count = 0;
    // let totalCount;
    // do {
    // axios.get(`http://openapi.seoul.go.kr:8088/${process.env.VUE_APP_API_KEY}/json/NanumcarSpotList/${startNumber}/${endNumber}`)
    //   .then((response) => {
    //     console.log(response.data.NanumcarSpotList.row);
    //     this.carInfoList = [...this.carInfoList, response.data.NanumcarSpotList.row];
    //     // console.log(Math.ceil(response.data.NanumcarSpotList.list_total_count / 1000));
    //     // totalCount = response.data.NanumcarSpotList.list_total_count;
    //     console.log(this.carInfoList);
    //   })
    //   .catch((error) => console.log(error));
    // startNumber = +1000;
    // endNumber = +1000;
    // eslint-disable-next-line no-unused-vars
    // count = +1;
    // } while (count <= 2);
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
