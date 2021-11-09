<template>
  <div class="chartComponent">
    <div class="col-md-12 field is-grouped">
        <p class="initiator-heading-line">Monthly Sales</p>
      <div class="control">
        <label class="checkbox">
          <select class="select-dropdown"
            v-model="selectedPlaceForChart"            
            @change="selectedPlacePush(selectedPlaceForChart)">
            <option disabled value="">Please select one</option>
            <option value="North">North</option>
            <option value="South">South</option>
            <option value="East">East</option>
            <option value="West">West</option> 
          </select>             
        </label>
      </div>  
    </div>
    <line-chart
      :width="1059"
      :height="179"
      :labels="['Jan', 'Feb', 'Mar', 'Apr', 'May','Jun','Jul','Sep','Oct','Nov','Dec']"
      :datasets="displayedDatasets">
    </line-chart>
  </div>
</template>

<script>

import LineChart from './LineChart';
import data from '../../public/Data Set - Insurance Client.json'
export default {
  name: 'monthly-conversion-chart',
  components: {
    LineChart
  },
  data() {
    return {
      selectedPlaceForChart:'North', 
      monthlyChartSelectedArray : [
          {
            label: '',
            borderColor: 'rgba(50, 115, 220, 0.5)',
            backgroundColor: 'rgba(50, 115, 220, 0.1)',
            data: []
          }
      ]
    }
  },

  created(){
    this.dataForChart()
  },

  computed: {
    displayedDatasets() {
      return this.monthlyChartSelectedArray
    } 
  },

  methods: {
    dataForChart () {
    var months=[]
    let selection = data.filter(el=>el['Customer_Region']===this.selectedPlaceForChart)
    for (var i=1;i<=12;i++){
        months[i-1]=selection.filter(e=>{
            console.log("date:::::"+e['Date of Purchase'].split('/')[0]+'/////'+i.toString())
            return i.toString()===e['Date of Purchase'].split('/')[0]
        })
    }
    this.loadChartData(months)
    },

    loadChartData (response) {
       let month = {}
       let dataChart = [];
       month = response
       month.forEach((el)=>{
          dataChart.push(el.length)
       })
       this.monthlyChartSelectedArray = [
          {
            label: 'month',
            borderColor: 'rgba(50, 115, 220, 0.5)',
            backgroundColor: 'rgba(50, 115, 220, 0.1)',
            data: dataChart
          }
        ] 
    },
   
    selectedPlacePush () {
      this.dataForChart ()
    },
  }


}
</script>
<style>
.chartComponent{

}
  
</style>
