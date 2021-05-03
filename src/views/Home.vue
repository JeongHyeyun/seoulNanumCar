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
      :covidCenter="covidCenter"
    />
  </div>
</template>

<script>
// @ is an alias to /src
/* eslint-disable no-loop-func */
import locationMap from '@/components/map.vue';
import locationLists from '@/components/list.vue';
import axios from 'axios';

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
      covidCenter: [],
    };
  },
  computed: {
  },
  methods: {
    /**
     * 데이터 로드하기
     */
    async loadData() {
      this.covidCenter = []; // 초기화
      const startNumber = 1; // 시작넘버
      const endNumber = 1000; // 끝넘버
      let count = 0; // 카운트 수
      let totalCount; // 전체 리스트 / 10의 올림 (리스트는 한 번에 10개 씩 가져올 수 있음)
      // await axios.get(`http://openapi.seoul.go.kr:8088/${process.env.VUE_APP_API_KEY}/json/NanumcarSpotList/${startNumber}/${endNumber}`)
      do {
        // eslint-disable-next-line no-await-in-loop
        await axios.get(`http://api.odcloud.kr/api/15077586/v1/centers?page=${startNumber}&perPage=${endNumber}&serviceKey=${process.env.VUE_APP_COVID_API_KEY}`)
          .then((response) => {
            this.covidCenter = [...this.covidCenter, ...response.data.data]; // 리스트 저장
            if (!totalCount) { // 불필요한 계산을 막기 위함
              totalCount = Math.ceil(response.data.totalCount / 100);
            }
          })
          .catch((error) => console.log(error));
        // startNumber += 1000; // 시작넘버 + 1000
        // endNumber += 1000; // 끝넘버 + 1000
        // eslint-disable-next-line no-unused-vars
        count += 1; // loop 돌아온 수
      } while (count < totalCount); // loop 돌아온 수가 돌아야 할 수 보다 적을 때, 한 번 돌기
    },
  },
  created() {
    this.loadData();
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
