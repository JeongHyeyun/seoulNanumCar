<template>
  <div id="map-wrap">
    <div id="map" style="widht: 500px; height: 500px;"></div>
  </div>
</template>

<script>
export default {
  mounted() {
    if (window.kakao && window.kakao.maps) { // kakao map이 있을 때,
      const container = document.getElementById('map'); // 지도 그릴 곳
      const options = { // 기본 옵션
        center: new kakao.maps.LatLng(33.450701, 126.570667), // 위도,경도
        level: 3, // 축소
      };
      const map = new kakao.maps.Map(container, options); // 지도 생성
      map.setMapTypeId(kakao.maps.MapTypeId.HYBRID);
    } else { // kakao map이 없을 때,
      const script = document.createElement('script');
      /* global kakao */
      script.onload = () => kakao.maps.load(this.initMap);
      script.src = `http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=${process.env.VUE_APP_KAKAO_MAP_KEY}`;
      document.head.appendChild(script);
    }
  },
  methods: {
  },
  created() {
  },
};
</script>

<style>

</style>
