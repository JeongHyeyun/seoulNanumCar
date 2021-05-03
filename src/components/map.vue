<template>
  <div id="map-wrap">
    <div id="map" style="widht: 500px; height: 500px;"></div>
  </div>
</template>

<script>
export default {
  props: ['covidCenter'],
  data() {
    return {
      map: null,
    };
  },
  computed: {
  },
  methods: {
    /**
     * 마커 그리기
     * @param {Object} location - 위치 {위도,경도}
     * @param {Boolean} inInit - 초기 로딩 여부
     */
    drawLocation(location, isInit = false) {
      const marker = new kakao.maps.Marker({ // 마커 그리기
        position: location, // 그리는 곳 주소
      });
      marker.setMap(this.map); // 지도에 마커 표시
      if (isInit) this.map.setCenter(location); // 마커가 표시된 곳으로 지도 중심 이동
    },
  },
  created() {
    setTimeout(() => { // 데이터 불러오는 로드의 시차
      // eslint-disable-next-line no-restricted-syntax
      for (const car of this.covidCenter) {
        const location = new kakao.maps.LatLng(car.lng, car.lat);
        this.drawLocation(location); // 맵에 그려주기
      }
    }, 1000);
  },
  mounted() {
    /**
     * 지도 그리기
     */
    const container = document.getElementById('map'); // 지도 그릴 곳
    const options = { // 기본 옵션
      center: new kakao.maps.LatLng(33.450701, 126.570667), // 위도,경도
      level: 3, // 축소
    };
    if (window.kakao && window.kakao.maps) { // kakao map이 있을 때,
      this.map = new kakao.maps.Map(container, options); // 지도 생성
      this.map.setMapTypeId(kakao.maps.MapTypeId.ROADMAP); // 지도 보여주는 방식 - 일반지도
    } else { // kakao map이 없을 때,
      const script = document.createElement('script');
      /* global kakao */
      script.onload = () => kakao.maps.load(() => {
        this.map = new kakao.maps.Map(container, options); // 지도 생성
      });
      script.src = `http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=${process.env.VUE_APP_KAKAO_MAP_KEY}`;
      document.head.appendChild(script);
    }
    /**
     * 현재 위치 구하기
     */
    if (navigator.geolocation) { // 현재 위치를 구할 수 있는 조건일 때,
      navigator.geolocation.getCurrentPosition((position) => {
        const { latitude } = position.coords; // 위도
        const { longitude } = position.coords; // 경도
        const location = new kakao.maps.LatLng(latitude, longitude);
        this.drawLocation(location, true);
      });
    } else { // 현재 위치를 구할 수 없는 조건일 때,
      const location = new kakao.maps.LatLng(37.57821, 126.976936); // 광화문 좌표
      this.drawLocation(location, true);
    }
  },
};
</script>

<style>

</style>
