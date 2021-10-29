<template>
    <div class="weatherapp relative bg-green-500 text-white h-screen" >
      <div class=" flex justify-center " >
        <h1 class=" text-center mt-5 text-4xl  bg-gray-400  bg-opacity-25 p-4 rounded  text-green-100 "  >   Weather App</h1>
      </div>
      <div>
        <h4 class="mb-10 text-sm text-center" >check the current weather  of a city </h4>
      </div>
      <div class="flex flex-col text-center justify-center">
        <div class="flex flex-col justify-center text-center items-center " >
          <input placeholder="Enter City..." v-model="query"  @keypress="search" class=" w-70 h-8 border rounded outline-none  px-2 mb-2 flex justify-self-center text-green-500 " type="search"  name="searchWeather" id="weatherid">
        <button class="border rounded-md mt-2 mb-2 p-2 text-sm  text-gray-500  hover:bg-gray-400 hover:text-white  hover:p-3 " @click="searchClick" > Check Weather </button>
        </div>
        
        <div v-if="loading" >
          <Spin />
         
        </div>
          <div v-if="detail.cod == 404  " class="mt-3" >
           <h1 class="text-2xl mt-3 animate__animated animate__fadeInUp animate__delay-0s  " >Opps not a valid state ... please enter a valid location 😊 </h1>
        </div>
        
         <div v-if="detail.cod != undefined && loading == false ">
               <div v-if="this.detail.main != undefined " class="animate__animated animate__zoomIn animate__delay-0s" >
           

          
          <h4 class="text-3xl mt-5" >  {{ Math.round(detail.main.temp) }} <span>°C</span> </h4>
          <h4 class="mt-2" >  {{ detail.weather[0].main }} </h4>
            <div class=" flex justify-center text-center  items-center " >
              <img src="http://openweathermap.org/img/wn/10d@2x.png" class="animate__animated animate__flip animate__delay-1s" alt="">  
            </div>
            <h3  > {{ detail.name}},  {{ detail.sys.country }} </h3>
        </div>
          
         </div>
           
       
      </div>
      
      <div  class="absolute bottom-5 inset-x-0  flex justify-center" >
        <p class="text-center " > ichbinsieger </p>
        <div class="ml-3 mt-1" >  <a href="https://github.com/ichbinsieger" class="mr-2" > <ion-icon name="logo-github"></ion-icon> </a>  <a href="https://twitter.com/ichbinsieger"><ion-icon name="logo-twitter"></ion-icon></a> </div>
      </div>
     </div>

     
       
   
</template>

<script>
import Spin from './components/Spin.vue'
import './index.css'

export default {
  
  
  data(){
     return{
       location: "lagos,Nigeria",
       api_key: "550d972c6e25316a8a59ad0f07c6c237",
       base_url: "https://api.openweathermap.org/data/2.5/",
       query: "",
       detail: {},
       url: '',
       loading: false
       
       
     }
  },
  methods:{
     
      search(e){
           if ( e.key == "Enter"  ) {
             this.loading  = true;
                 setTimeout( () => { this.loading = false } , 1000);
                 setTimeout(() =>  { fetch( `${this.base_url}weather?q=${this.query}&units=metric&appid=${this.api_key}`).then(response => response.json()).then( this.results) } , 1000);
                 
                 
                  

           

           }
            
      },
      searchClick(){
          
              this.loading  = true;
                 setTimeout( () => { this.loading = false } , 1000);
                 setTimeout(() =>  { fetch( `${this.base_url}weather?q=${this.query}&units=metric&appid=${this.api_key}`).then(response => response.json()).then( this.results) } , 1000);
                 
      },
      results(result){
          this.detail =  result
         this.url = `http://openweathermap.org/img/wn/${this.detail.weather[0].icon}@2x.png`
       },
       
     
      

  
      
     
  },
 components:{
   Spin,
 }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');

.weatherapp{
  font-family: 'Montserrat', sans-serif;
}

</style>
