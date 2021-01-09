<template>
  <div>
    <div id="mymap"></div>
  </div>
</template>

<script>
// Leaflet
import L from 'leaflet';
import "leaflet/dist/leaflet.css";

export default{
  name: "vmap",
  mounted: function(){
    this.map = L.map("mymap");
    this.map.setView(this.latlng, this.scale);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(this.map);

    //円を描く(MT44からの位置情報)
    L.circle([35.60643, 139.74891], {
    color: 'red',
    fillColor: '#f03',
    fillOpacity: 0.5,
    radius: 300
    }).addTo(this.map);
    
    //マーカを表示(Supressenceの位置)
    var currentPosi=L.marker([35.60643, 139.74891]).addTo(this.map);
    currentPosi.bindPopup("<p>Your are here</p>").openPopup();
    this.todo();
  },
  data: function(){
    return{
      latlng: [35.60643, 139.74891],
      scale: 16,
      disasters:null
    }
  },
  methods:{
     todo : function(){
        var sse = new EventSource("/sse");
        var self=this;
        
        sse.onmessage = function (evt) {
        localStorage.setItem('env',evt.data);
        var jsonObj = localStorage.getItem('env');
        self.disasters=JSON.parse(jsonObj);
        //localStorage.clear();
        
        //self.disasters=JSON.parse(localStorage.getItem('env'));  
        console.log(self.disasters)
       }
    }
  }
}
</script>
 
<style scoped>
#mymap{
  width: 480px;
  height: 480px;
  margin-left: auto;
  margin-right: auto;
}
</style>