<template>
  <div id="app">
    <div class="col-md-7">
      <b-input-group>
        <b-form-input :class="isMobile() ? 'mobileInput' : 'dateInput'" v-on:blur="findDates" v-model="startToEndDates" placeholder="YYYY/MM/DD-YYYY/MM/DD">
        </b-form-input>
        <b-input-group-append>
          <b-button :class="isMobile() ? 'mobileSearch' : 'searchButton' " @click="findResults()">
            <b-img 
            src="icon_search.svg"
            contain
            height = "20"
            weight = "20"
            :class="isMobile() ? 'mobileSearchIcon' : ''"
            >
            </b-img>
          </b-button>
        </b-input-group-append>
      </b-input-group>
    </div>
    <div class="text-left">
      <span :class="isMobile() ? 'mobRes' : 'res'"> Results : <span :class ="isMobile() ? 'mobResText' : 'resultText'"> {{numResults}}</span>mail(s)</span>
    </div>
    <div v-if ="isMobile() === false">
      <Desktop :results="results" :numResults="numResults" :fields="fields" :sortBy ="sortBy" :sortDesc="sortDesc"/>
    </div>
    <div v-else>
      <Mobile :results="orderedResults" :numResults="numResults" :fields="fields" :sortBy ="sortBy" :sortDesc="sortDesc"/>
    </div>
  </div>
</template>

<script>
import * as moment from "moment/moment";
import Desktop from "./components/Desktop"
import Mobile from  "./components/Mobile"
export default {

  name: 'App',
  components: {Desktop, Mobile},
  data(){
    return{
      mobileMedia : false,
      startToEndDates : "2019/12/27 - 2020/01/09",
      numResults : 0,
      startDate: null,
      endDate: null,
      sortBy :'date',
      sortDesc : true,
      isHovered :false,
      body:`Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor 
            incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
            exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
            dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
            Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit
            anim id est laborum.`,
      fields : [
                {key :'from',sortable:false, class: "fromCol"},
                {key :'to',sortable:false, class: "toCol"},
                {key :'subject',sortable:false, class:"subjectCol"},
                {key :'formatDate', label : "Date" ,sortable:false, class:"dateText"}
                ],
      
      emails : [
                {from:'aaa@example.com', to:['zzz.zzz@example.com','abc.def@example.com','zyz@example.com'], subject:'Notice of offical announcemnet',date :'2020-01-09 12:30', attachments : true, body:`Lorem ipsum dolor sit amet, 
                consectetur adipiscing elit, sed do eiusmod tempor`, _showDetails:false, active:false},

                {from:'abc@example.com', to:['abc.def@example.com','zzz.zzz@example.com','zyz@example.com'], subject:'Web Contract',date :'2020-01-01 12:30', attachments : false, body:`incididunt ut labore et dolore magna aliqua.
                 Ut enim ad minim veniam, quis nostrud`, _showDetails:false, active:false},

                {from:'dc.wfwefe@example.com', to:['zyz@example.com'], subject:'Happy New Year',date :'2020-01-03 12:30', attachments : false, body:`exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure
                `, _showDetails:false, active:false},

                {from:'ghi@example.com', to:['opm@example.com','xyz@example.com'], subject:'[Github] Logout page',date :'2020-01-04 12:30', attachments : true, body:`dolor in reprehenderit in voluptate velit esse cillum dolore eu 
                fugiat nulla pariatur.`, _showDetails:false, active:false},

                {from:'xyz.frgsa@example.com', to:['qrs.asz@example.com','xyz@example.com'], subject:'Re: [Github] Brush-up on loading animation ',date :'2020-01-05 12:30', attachments : false, body:`Excepteur sint occaecat cupidatat non proident,
                 sunt in culpa qui officia deserunt mollit`, _showDetails:false, active:false},

                {from:'dw.dfgs@example.com', to:['abd.ull@example.com'], subject:'[info:888] ABC EQUIPMENT COMPANY',date :'2020-01-06 12:30', attachments : true, body:`dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
                Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.`, _showDetails:false, active:false},

                {from:'aa1a@example.com', to:['zzz.zzz@example.com','abc.def@example.com','zyz@example.com','def.ghi@example.com'], subject:'Notice of offical announcemnet',date :'2019-12-29 12:30', attachments : true, body:`Excepteur sint occaecat cupidatat non proident, 
                sunt in culpa qui officia deserunt mollit`, _showDetails:false, active:false},

                {from:'ab2c@example.com', to:['abc.def@example.com','zzz.zzz@example.com','zyz@example.com'], subject:'Web Contract',date :'2019-12-27 12:30', attachments : false, body:`Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
                 officia deserunt mollit`, _showDetails:false, active:false},

                {from:'dc3.wfwefe@example.com', to:['zyz@example.com'], subject:'Happy New Year',date :'2019-12-27 12:30', attachments : false, body:`incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud
                exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure`, _showDetails:false, active:false},

                {from:'ghi1@example.com', to:['opm@example.com','xyz@example.com'], subject:'[Github] Logout page',date :'2019-12-28 12:30', attachments : true, body:`exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure`
                , _showDetails:false, active:false},

                {from:'xyz2.frgsa@example.com', to:['qrs.asz@example.com','xyz@example.com'], subject:'Re: [Github] Brush-up on loading animation ',date :'2019-12-31 12:30', attachments : false, body:`Lorem ipsum dolor sit amet, consectetur adipiscing elit, 
                sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud`, _showDetails:false, active:false},

                {from:'d5w.dfgs@example.com', to:['abd.ull@example.com'], subject:'[info:888] ABC EQUIPMENT COMPANY',date :'2020-01-12 12:30', attachments : true, body:`Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor 
                 incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud`, _showDetails:false, active:false},

                ],
      results : []
    }
  },
  methods:{
    findDates(){
      var dates = this.startToEndDates.split("-")
      this.startDate = moment(dates[0])
      this.endDate = moment(dates[1])
      console.log(this.startDate,this.endDate)
    },
    findResults(){
      this.results = []
      this.findDates()
      this.emails.forEach(e=> {
        if(moment(e.date).isSameOrAfter(this.startDate,'day') && moment(e.date).isSameOrBefore(this.endDate,'day')){

          if(moment(e.date).isSame(this.endDate,'day')){
            e.formatDate = moment(e.date).format('H:mm')
          }else if(moment(e.date).isSame(this.endDate,'year')){
            e.formatDate = moment(e.date).format('MMM DD')
          }else{
            e.formatDate = moment(e.date).format('YYYY/DD/MM')
          }

          this.results.push(e)
        }
      });
      console.log(this.results)
      this.numResults = this.results.length
    },
    isMobile() {
      if( screen.width <= 760 ) {
          return true;
      }
      else {
          return false;
      }
    }
  }, 
  computed: {
    orderedResults: function () {
      return this.results.slice().sort((a,b)=>(a.from > b.from ? 1: -1));
    }
  }  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  padding-left : 20px
}
.mobileInput{
  max-width: 60% !important;
  border-color:#A9A9A9 !important;
  padding:10px  !important;
  padding-left: 10% !important;
  background-image:url("/icon_calender.svg") !important;
  background-position: 5px 5px !important;
  background-repeat: no-repeat !important;
  background-size: 20px 20px !important;
  font-size: 13px !important;
  position: relative;
  left : -20px;
}

.dateInput{
  max-width: 45% !important;
  border-color:#A9A9A9 !important;
  padding: 20px !important;
  padding-left: 5% !important;
  background-image:url("/icon_calender.svg") !important;
  background-position: 10px 10px !important;
  background-repeat: no-repeat !important;
  background-size: 20px 20px !important;
}
.mobileSearch{
  color: #D3D3D3 !important;
  background-color: #e9e9e9 !important;
  border-color:#A9A9A9 !important;
  padding-left : 10px !important;
  padding-right: 15px !important;
  padding-top : 0px !important;
  padding-bottom: 0px !important;
  position: relative !important;
  left: -20px
}
.mobileSearchIcon{
  height : 15px;
  width : 15px;
  
}
.searchButton{
  color: #D3D3D3 !important;
  background-color: #e9e9e9 !important;
  border-color:#A9A9A9 !important;
  padding-left : 20px !important;
  padding-right: 20px !important;
}

.resultText{
  font-size: 16pt;
}
.mobResText{
  font-size: 14pt;
}
.res{
  padding-left : 15px;
  display: inline-block;
  color: rgb(95, 95, 95);
  font-weight:bolder;
  font-size: 12pt;
  text-align: left;
}
.mobRes{
  display: inline-block;
  color: rgb(95, 95, 95);
  font-weight:bolder;
  font-size: 10pt;
  text-align: left;
}
</style>
