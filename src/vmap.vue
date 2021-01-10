<template>
  <div>
    <h1 class=box1>Disaster information </h1>
      <table class="table">
      <thead class="thead-lignt">
      <tr>
        <th>Message Type</th>
        <th>Disaster Category</th>
        <th>Guide To React</th>
      </tr>
      </thead>
        <tbody>
       <tr v-for="disaster in disasters" v-bind:key="disaster">
        <td> {{disaster.messageType}}</td>
        <td> {{disaster.disasterCategory}}</td>  
        <td> </td>
        <v-for/>
        </tr>
        </tbody>
      </table>
      <h1 class=box1>Disaster area map </h1>
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
    this.todo();
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
        var jsonParse=JSON.parse(jsonObj);
        self.disasters=jsonParse.slice().reverse().slice(0,1);
        //localStorage.clear()
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
table{
  border-collapse: collapse;
  border-spacing: 0;
  table-layout: fixed;
  width: 490px;
  margin-left: auto;
  margin-right: auto;
}

table tr:last-child{
  border-bottom:solid 1px #ddd;
}

table th{
  text-align: center;
  padding: 7px 0;
  border-right:solid 1px #ddd;
  border-left:solid 1px #ddd;
  width: 155px;
}

table th:nth-child(1){
  background-color:#dddddd;
}

table th:nth-child(3){
  background-color:#f5b932;
  color: white;
}

table tr:nth-child(2) td{
  font-size: 30px;
}

table td{
  text-align: center;
  padding: 7px 0;
  border-right:solid 1px #ddd;
  border-left:solid 1px #ddd;
  width: 155px;
}

table td a{
  background-color: #25b327;
  color: white;
  padding:5px 20px;
  border-radius: 30px;
  font-weight: bold;
}

table .popular{
  width: 180px;
}

table th.popular{
  position: relative;
}

table th.popular span.no1{
  position: absolute;
  top: -10px;
  left:calc(50% - 30px);
  background: #bdcc28;
  width: 60px;
  font-size: 10px;
  border-radius: 15px;
  line-height: 1;
  padding: 5px;
}

table th.popular span.inner{
  position: absolute;
  color:white;
  background-color: #f34955;
  left: 0;
  bottom: 0;
  display: block;
  width: 180px;
  padding: 10px 0;
}
h1{
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  font-size:large;
}
.box1{
    padding: 8px 19px;
    margin: 2em 0;
    color: #2c2c2f;
    background: #cde4ff;
    border-top: solid 5px #5989cf;
    border-bottom: solid 5px #5989cf;
}
.box1 h1 {
    margin: 0; 
    padding: 0;
}
</style>

