<template>
  <div id="map">
    <div id="test" style="widht: 500px; height: 500px;"></div>
  </div>
</template>

<script>
export default {
  mounted() {
    if (window.kakao && window.kakao.maps) {
      const container = document.getElementById('test');
      const options = {
        center: new kakao.maps.LatLng(33.450701, 126.570667),
        level: 3,
      };
      const map = new kakao.maps.Map(container, options);
      map.setMapTypeId(kakao.maps.MapTypeId.HYBRID);
    } else {
      const script = document.createElement('script');
      /* global kakao */
      script.onload = () => kakao.maps.load(this.initMap);
      script.src = 'http://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=31d511183ce76554f7d189a8659e629d';
      document.head.appendChild(script);
    }
  },
  methods: {
    init() {
      console.log('init');
    },
    add() {
      console.log('add');
    },
  },
};
</script>

<style>

</style>
