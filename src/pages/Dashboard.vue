<template>
   <el-container class="root">
     <!-- Sibe bar -->
      <el-aside class="side-bar" width="350px">
        <el-row class="session-one-aside">
          <el-col :span="20" >
            <el-input 
              type="text"
              placeholder="Type something" 
              v-model="query" 
              @keypress="fetchDataWeather"
            >
              <template #prefix>
                <el-icon class="el-input__icon">
                  <svg class="icon" width="200" height="200" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg"><path fill="currentColor" d="M795.904 750.72l124.992 124.928a32 32 0 01-45.248 45.248L750.656 795.904a416 416 0 1145.248-45.248zM480 832a352 352 0 100-704 352 352 0 000 704z"></path></svg>
                </el-icon>
              </template> 
            </el-input>
          </el-col>
          <el-col class="hidden-md-only" :span="4">
            <svg class="icon" width="24" height="24" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" data-v-365b8594=""><path fill="currentColor" d="M926.784 480H701.312A192.512 192.512 0 00544 322.688V97.216A416.064 416.064 0 01926.784 480zm0 64A416.064 416.064 0 01544 926.784V701.312A192.512 192.512 0 00701.312 544h225.472zM97.28 544h225.472A192.512 192.512 0 00480 701.312v225.472A416.064 416.064 0 0197.216 544zm0-64A416.064 416.064 0 01480 97.216v225.472A192.512 192.512 0 00322.688 480H97.216z"></path></svg>
          </el-col>
        </el-row>
  
        <el-row class="session-two-aside">
          <el-row style="width: 100%">
            <el-col :span="4"></el-col>
            <el-col :span="10">
              <img  src="../assets/Weather/cloudy.png" />
               <!-- <img style="width: 50px" src="//cdn.weatherapi.com/weather/64x64/day/116.png" /> -->
            </el-col>
            <el-col :span="6" ></el-col>
          </el-row>
          <el-col align="center" :span="24"><span class="temp-aside">12°</span></el-col>  
          <el-col align="center" :span="24"><span class="day-aside">Monday,</span><span class="time-aside">16:00</span></el-col>
          <el-divider></el-divider>
          <el-row style="width: 100%" justify="center">
            <el-col  :span="10">
              <div class="status-aside">
                <img  style="width: 24px; margin-right: 10px" src="../assets/Weather/cloud.png" />
                <span class="desc-aside"> Mostly cloudy</span>
              </div>
            </el-col>
          </el-row>
          <el-row style="width: 100%" justify="center">
            <el-col :span="10">
              <div class="status-aside">
                <img  style="width: 24px; margin-right: 10px" src="../assets/Weather/rain.png" />
                <span class="rain-aside" >Rain - 30%</span>
              </div>
            </el-col>
          </el-row>
          <el-divider></el-divider>
          <el-row>
            <img  style="width: 218px; margin-right: 10px; border-radius: 20px" src="../assets/Weather/newyork.jpg" />
          </el-row>
        </el-row>
      </el-aside>
      <!-- End side bar -->
      <el-container class="parent-container">
          <!-- Header -->
          <el-header>
            <el-row>
              <el-col :span="20">
                <span style="font-weight: 900; font-size: 20px">7 days</span>
              </el-col>
              <el-col :span="3" style="padding-left: 20px">
                <el-button style="background-color: black; color: white; font-weight: 600; border:none" circle>°C</el-button>
                <el-button style="background-color: white; color: black; font-weight: 600; border:none" circle>°F</el-button>
              </el-col>
              <el-col :span="1">
                <img  style="width: 42px; border-radius: 10px" src="../assets/Weather/unnamed.webp" />
              </el-col>
            </el-row>
          </el-header>
          <!-- End header -->
          <el-main>
            <el-row justify="space-between" class="session-card-weather-day">
              <el-col  v-for="item in weatherInWeek" :key="item" :span="3">
                <el-card class="card-weather-day">
                  <el-row justify="center">
                    <span class="status-card" >{{item.day}}</span>
                  </el-row>
                  <el-row justify="center">
                    <img :src="item.img"/>
                    <!-- <img :src="item.img"/> -->
                  </el-row>
                  <el-row justify="center"> 
                    <span class="temp-card">{{item.dayTimeTemp}}°</span>
                    <span class="temp-card" style="color: blue; margin-left: 10px">{{item.nightTemp}}°</span> 
                  </el-row>
                </el-card>
              </el-col >
            </el-row>
            <el-row class="title-details"  >
              <el-col :span="24">
                <span class="title-details">Today's Highlights</span>
              </el-col>
            </el-row>
            <el-row  class="session-details">
             <el-row justify="space-between" style="width: 100%; margin-bottom: 40px">
                <el-col :span="7">
                  <el-card class="card-details-uv">
                    <el-row>
                      <span> UV Index </span>
                    </el-row>
                    <el-row justify="center" style="margin-top: 20px">
                      <el-progress  :stroke-width="26" type="dashboard" :percentage="30" color="#ffd347" />
                    </el-row>
                  </el-card>
                </el-col>
              <el-col :span="7">
                <el-card class="card-details-wind">
                  <el-row  class="title-card">
                    <span> Wind Status </span>
                  </el-row>
                   <el-row  class="body-card">
                    <span > 7.70 <span style="font-size: 30px">km/h</span> </span>
                  </el-row>
                   <el-row  class="footer-card">
                   <svg class="icon" style="color: violet; margin-right: 20px; border-radius: 40px; border: 1px solid gray" width="24" height="24" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" data-v-365b8594=""><path fill="currentColor" d="M512 928c23.936 0 117.504-68.352 192.064-153.152C803.456 661.888 864 535.808 864 416c0-189.632-155.84-320-352-320S160 226.368 160 416c0 120.32 60.544 246.4 159.936 359.232C394.432 859.84 488 928 512 928zm0-435.2a64 64 0 100-128 64 64 0 000 128zm0 140.8a204.8 204.8 0 110-409.6 204.8 204.8 0 010 409.6z"></path></svg>
                    <span> WSW</span>
                  </el-row>
                </el-card>
              </el-col>
              <el-col :span="7">  
                <el-card class="card-details-sun">
                    <el-row  class="title-card">
                      <span> SunRise and SunSet </span>
                    </el-row>
                    <el-row  class="body-card">
                      <el-col  :span="24">
                        <el-row style="align-items: center; margin-bottom: 20px">
                          <img src="../assets/Weather/up-arrow.png" />
                          <span style="margin-left: 20px;font-weight: 600; font-size: 20px">06:35 AM</span>
                        </el-row>
                      </el-col>
                      <el-col :span="24">
                       <el-row style="align-items: center">
                        <img src="../assets/Weather/up-arrow.png" />
                        <span style="margin-left: 20px;font-weight: 600; font-size: 20px">05:26 PM</span>
                       </el-row>
                      </el-col>
                    </el-row>

                  </el-card>
              </el-col>
             </el-row>
               <el-row justify="space-between" style="width: 100%">
                <el-col :span="7">
                  <el-card class="card-details-humidity">
                    <el-row  class="title-card">
                      <span> Humidity </span>
                    </el-row>
                    <el-row  class="body-card">
                      <el-col :span="20">
                      <span style="font-size: 50px; font-weight: 800" > 12 <span style="font-size: 30px">%</span> </span>
                      </el-col>
                       <el-col :span="4">
                        <img style="width: 50px;" src="../assets/Weather/Humidity-icon.png" />
                      </el-col>
                    </el-row>
                    <el-row  class="footer-card">
                      <span> Normal</span>
                    </el-row>
                  </el-card>
              </el-col>
              <el-col :span="7">
                <el-card class="card-details-humidity">
                    <el-row  class="title-card">
                      <span> Visibility </span>
                    </el-row>
                    <el-row  class="body-card">
                       <el-col :span="20">
                      <span style="font-size: 50px; font-weight: 800" > 5.2 <span style="font-size: 30px">km</span> </span>
                       </el-col>
                        <el-col :span="4">
                        <img style="width: 50px;" src="../assets/Weather/776008.png" />
                      </el-col>
                    </el-row>
                    <el-row  class="footer-card">
                      <span> Average</span>
                    </el-row>
                  </el-card>
              </el-col>
              <el-col :span="7">   <el-card class="card-details-humidity">
                    <el-row  class="title-card">
                      <span> Air quality </span>
                    </el-row>
                    <el-row  class="body-card">
                      <el-col :span="20">
                        <span style="font-size: 50px; font-weight: 800" > 105 <span style="font-size: 30px"></span> </span>
                      </el-col>
                      <el-col :span="4">
                        <img style="width: 50px;" src="../assets/Weather/images.png" />
                      </el-col>
                    </el-row>
                    <el-row  class="footer-card">
                      <span> Unhealthy</span>
                    </el-row>
                  </el-card></el-col>
             </el-row>
            </el-row>
            
          </el-main>
        </el-container>
      </el-container>
</template>
<script>
import {LocationFilled} from '@element-plus/icons-vue'
export default {
  components:{
  },
  data(){
    return {
      api_key: 'd92f8ceffa5b449db0942837213012',
      url_base: 'https://api.weatherapi.com/v1/',
      query:'',
      weather: {},
      weather7Days: {},
      weatherInWeek: [
        {day: "Sun", img: require("../assets/Weather/sun.png"),dayTimeTemp: 15, nightTemp: -3},
        {day: "Mon", img: require("../assets/Weather/cloudy (1).png"),dayTimeTemp: 12, nightTemp: -7},
        {day: "Tue", img: require("../assets/Weather/rain.png"),dayTimeTemp: 9, nightTemp: -7},
        {day: "Wed", img: require("../assets/Weather/cloud.png"),dayTimeTemp: 9, nightTemp: 5},
        {day: "Thu", img: require("../assets/Weather/windy.png"),dayTimeTemp: 4, nightTemp: -4},
        {day: "Fri", img: require("../assets/Weather/sun.png"),dayTimeTemp: 7, nightTemp: -3},
        {day: "Sat", img: require("../assets/Weather/cloud.png"),dayTimeTemp: 10, nightTemp: -8},
      ],
      LocationFilled
    }
  },
  created() {
    this.fetchWeather7days()
  },
  methods:{ 
    fetchWeather7days(){
       fetch(`${this.url_base}forecast.json?key=${this.api_key}&q=London&days=7&aqi=yes&alerts=yes`)
          .then(res =>{
            return res.json()
          }).then(result => {
            console.log(result);
            this.weather7Days = result
          })
    },
    fetchDataWeather (ev){
      if (ev.key === "Enter"){
        fetch(`${this.url_base}current.json?key=${this.api_key}&q=${this.query}&aqi=yes`)
          .then(res =>{
            return res.json()
          }).then(result => {
            console.log(result);
            this.weather = result
          })
      }
    }
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300&display=swap');
*{
  margin: 0;
  font-family: 'Lato', sans-serif;
}
.root{
  min-height: 100vh;
}
.session-one-aside{
  margin-top: 20px;
  padding: 0 30px 0 40px;
  align-items: center;
}
.session-one-aside .el-input__inner{
  border: none;
  color: black;
  font-weight: 600;
  margin-left: 10px;
}

.session-one-aside .el-icon{
  color: black;
  font-weight: 900;
  font-size: 20px;
}
.session-two-aside{
  margin-top: 40px;
  justify-content: center;
}
.session-two-aside img{
  width: 200px;
}
.session-two-aside .temp-aside{
  font-size: 100px;
  font-weight: 900;
}
.session-two-aside .day-aside{
  font-weight: 600;
  font-size: 20px;
}
.session-two-aside .time-aside{
  font-weight: 400;
  font-size: 20px;
  color: gray;
  margin-left: 10px;
}
.status-aside{
  display: flex;
  font-weight: 600;
  align-items: center;
}
/* main */
/* header */

.parent-container{
  background-color: #f7f6f9;
  padding: 0 30px 0 40px
}
.el-header{
  margin-top: 20px;
  align-items: center;
}
.el-header img{
  float: right;
  /* margin-left: 20px; */
}
.el-main .card-weather-day{
  border-radius: 20px;
}
.status-card{
  font-weight: 900;
  font-size: 20px;
  margin-bottom: 20px;
}
.temp-card{
  margin-top: 15px;
  font-weight: 600;
  font-size: 18px;
}
.card-weather-day img{
  width: 88px
}
.title-details{
  margin-top: 60px;
  margin-bottom: 30px;
  font-size: 18px;
  font-weight: bolder;
}
.el-main .el-card__body {
  min-height: 138px;

}
.el-main .card-details-uv{
  border-radius: 15px;
}
.el-main .card-details-uv span{
  font-size: 20px;
  color: gray;
}
.el-main .card-details-wind{ 
  border-radius: 15px;
}
.card-details-wind .title-card{
   font-size: 20px;
    color: gray;
}
.card-details-wind .body-card {
  padding: 30px 0;
  font-size: 50px;
  font-weight: 900;
}
.card-details-wind .footer-card{
  font-weight: 900;
  font-size: 18px;
  margin-bottom: 5px;
}
.el-main .card-details-sun{
  border-radius: 15px;
}
.card-details-sun .title-card{
   font-size: 20px;
    color: gray;
}
.card-details-sun .body-card{
  padding: 32px
}
.card-details-sun .body-card img{
  width: 32px;
}
.el-main .card-details-humidity{
  border-radius: 15px;
}
.card-details-humidity .title-card{
   font-size: 20px;
    color: gray;
}
.card-details-humidity .body-card{
  padding: 20px
}
.card-details-humidity .footer-card{
  font-weight: bold;
}
</style>