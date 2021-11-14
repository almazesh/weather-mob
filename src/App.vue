<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : '' ">
      <main>
          <div class="searchBox">
              <input
                v-model="query"
                type="text"
                placeholder="Town"
                class="search_bar"
                @keypress="fetchWeather"
                
                />
          </div>

          <div class="weather-wrap" v-if="typeof weather.main != `undefined`">
              <div class="location-box">
                <div class="location">
                    {{weather.name}} , {{weather.sys.country}}
                </div>
                <div class="date">
                    {{dataBuilder()}}
                </div>
              </div>


              <div class="weather-box">
                  <div class="temp">{{Math.round(weather.main.temp)}}*c</div>
                  <div class="weather">{{weather.weather[0].main}}</div>
              </div>
          </div>
      </main>
  </div>
</template>

<script>
export default {
  cold:'https://wallpapercave.com/wp/wp3335304.jpg',
  warm:'https://wallpapercave.com/wp/wp3335304.jpg',
  components: {
    
  },
  data(){
    return{
      api_key:'fad1e58b685af671bf2a8bdb20dfb677',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key === 'Enter'){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => res.json())
        .then(r => this.setResult(r))
      }
    },

    setResult(response){
      this.weather = response;
    },

    dataBuilder(){
    let d = new Date();
    let months = ['January' , 'February' , 'March' , 'April' , 'May' , 'June' , 'Jule' , 'August' , 'September' , 'October' , 'November' , 'December']

    let days = ['Sunday' , 'Monday' , 'Tuesday' , 'Wednesday' , 'Thursday' , 'Friday' , 'Saturday']

    let day = days[d.getDay()]
    let date = d.getDate()
    let month = months[d.getMonth()]
    let year = d.getFullYear()

    return `${day} ${date} ${month} ${year}`
  }

  }
  


  
}

</script>



<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,200;0,400;0,500;0,600;1,400;1,500&display=swap');
    *{
      margin: 0;
      font-family: 'Montserrat', sans-serif;
    }

    

    #app{
      background: url('https://wallpapercave.com/wp/wp3335304.jpg') center / cover;
      width: 100%;
      height: 100vh;
    }

    #app.warm{
      background: url('https://i.pinimg.com/originals/4c/30/44/4c3044943bed698052992e569961abe7.jpg') center / cover;
      width: 100%;
      height: 100vh;
    }

    main{
      min-height: 100vh;
      background: linear-gradient(to bottom , rgba(0,0,0,0.25) , rgba(0,0,0,0.7));
    }

    .searchBox{
      width: 70%;
      margin: auto;
    }

    .searchBox input{
      width: 100%;
      display: block;
      padding: 15px;
      color: #313131;
      font-size: 20px;
      appearance: none;
      border:0;
      outline: 0;
      background: none;
      background-color: rgba(255,255,255,0.5);
      border-radius: 0 16px 0 16px;
      transition: 0.4s;
      box-shadow: 0 0 8px rgba(0,0,0,0.25);
    }

    .searchBox input:focus{
      box-shadow:  0 0 16px rgba(0,0,0,0.75);
      background-color: rgba(255,255,255,0.75);
      border-radius: 16px 0 16px 0;
    }



    .location-box .location{
      color: white;
      font-size: 32px;
      font-weight: 500;
      text-align: center;
      margin-top: 50px;
      text-shadow: 1px 3px rgba(0,0,0,0.25);
    }

    .location-box .date{
      color: white;
      font-size: 20px;
      font-weight: 300;
      text-align: center;
      margin-top: 10px;
      font-style: italic;
    }

    .weather-box{
        text-align: center;
    }

    .weather-box .temp{
      display: inline-block;
      padding: 10px 25px;
      color: white;
      font-size: 102px;
      margin:30px 0;
      border-radius: 16px;
      box-shadow: 3px 6px rgba(0,0,0,0.25);
      font-weight: 900;
      text-shadow:  3px 6px rgba(0,0,0,0.25);
      background-color: rgba(255,255,255,0.25);
    }

    .weather-box .weather{
      color: white;
      font-style: italic;
      font-size: 48px;
      font-weight: 700;
      text-shadow: 3px 6px rgba(0,0,0,0.25);
    }
</style>