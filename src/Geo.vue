<template>
    <div class="map-container">
        <h1>Геолокация</h1>
        <div id="map" style="width: 600px; height: 400px"></div>
    </div>
</template>
  
<script>
ymaps.ready(init);
    function init(){
        var myMap = new ymaps.Map("map", {
            center: [53.376505, 58.970608],
            zoom: 15,
            controls: ['routePanelControl']
        });

        var myGeoObject = new ymaps.GeoObject({
          geometry: {
          type: "Point", 
          coordinates: [53.376505, 58.970608]
          }
        });

        var control = myMap.controls.get('routePanelControl');

        control.routePanel.state.set({
            to: 'Улица Галиуллина, 16'
        });

        myMap.geoObjects.add(myGeoObject); 
    }
</script>

<style>

</style>