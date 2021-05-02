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
      :carInfoList="carInfoList"
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
      carInfoList: [],
    };
  },
  async created() {
    // json 불가하다고 함...
    // 다른 api로 바꿀 예정
    // axios.get(`http://openapi.seoul.go.kr:8088/${process.env.VUE_APP_API_KEY}/json/NanumcarCarList/1/1000/`)
    //   .then((response) => {
    //     console.log(response);
    //   });
    // /**
    //  * 데이터 로드하기
    //  */
    // let startNumber = 1; // 시작넘버
    // let endNumber = 1000; // 끝넘버
    // let count = 0; // 카운트 수
    // let totalCount; // 전체 리스트 / 1000의 올림 (리스트는 한 번에 천 개씩 가져올 수 있음)
    // do {
    //   // eslint-disable-next-line no-await-in-loop
    //   await axios.get(`http://openapi.seoul.go.kr:8088/${process.env.VUE_APP_API_KEY}/json/NanumcarSpotList/${startNumber}/${endNumber}`)
    //     .then((response) => {
    //       this.carInfoList = [...this.carInfoList, ...response.data.NanumcarSpotList.row];
    // 리스트 저장
    //       if (!totalCount) { // 불필요한 계산을 막기 위함
    //         totalCount = Math.ceil(response.data.NanumcarSpotList.list_total_count / 1000);
    //       }
    //     })
    //     .catch((error) => console.log(error));
    //   startNumber += 1000; // 시작넘버 + 1000
    //   endNumber += 1000; // 끝넘버 + 1000
    //   // eslint-disable-next-line no-unused-vars
    //   count += 1; // loop 돌아온 수
    // } while (count < totalCount); // loop 돌아온 수가 돌아야 할 수 보다 적을 때, 한 번 돌기
    // url 정보 변경 예정
    axios.get('https://infuser.odcloud.kr/oas/15077586')
      .then((response) => {
        console.log(response);
      });
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
