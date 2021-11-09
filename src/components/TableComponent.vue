<template>
    <div class="table-wrapper">
        <vue-good-table
            :columns="columns"
            :rows="rows"
            :pagination-options="{
                enabled: true
            }"
            :search-options="{
                enabled: true
            }"
            styleClass="vgt-table bordered"
            >
        </vue-good-table>
    </div>
</template>
<script>
// import axios from 'axios';
import { VueGoodTable } from 'vue-good-table';
import data from '../../public/Data Set - Insurance Client.json'
import 'vue-good-table/dist/vue-good-table.css'

export default {
    components:{
        VueGoodTable
    },
    data (){
        return{
            columns: [
            {
                label: 'Policy_id',
                field: 'Policy_id',
                type: 'number',
            },
            {
                label: 'Date of Purchase',
                field: 'Date of Purchase',
                dateInputFormat: 'MM/DD/YYYY',
                dateOutputFormat: 'DD/MM/YYYY',
            },
            {
                label: 'Customer_id',
                field: 'Customer_id',
                type: 'number',
            },
            {
                label: 'Fuel',
                field: 'Fuel',
            },
            {
                label: 'VEHICLE_SEGMENT',
                field: 'VEHICLE_SEGMENT',
            },
            {
                label: 'Premium',
                field: 'Premium',        
            },
            {
                label: 'Customer_Gender',
                field: 'Customer_Gender',
            },
            {
                label: 'Customer_Income group',
                field: 'Customer_Income group',
            },
            {
                label: 'Customer_Region',
                field: 'Customer_Region',
            },
            {
                label: 'bodily injury liability',
                field: 'bodily injury liability',
            },
            {
                label: 'personal injury protection',
                field: 'personal injury protection',
            },
            {
                label: 'property damage liability',
                field: 'property damage liability',
            },
            {
                label: 'collision',
                field: 'collision',
            },
            {
                label: 'comprehensive',
                field: 'comprehensive',
            },
            {
                label: 'Customer_Marital_status',
                field: 'Customer_Marital_status',
            },
            {
                label: 'edit',
                field: 'edit',
            },
            
            ],
            rows: [       
            ],
            text:''
        }
    },
    created(){
        this.getData();
    },
    methods:{
        getData(){
            // var res=[]
            // var headers={"Access-Control-Allow-Origin": "*","origin":"http://127.0.0.1"}
            // axios.get('http://127.0.0.1:5000/',headers)
            // .then((response)=>{
            //     this.loadData(response.data)
            // })
            // .catch((response) => {  
            //     res=data
            //     console.log("Error"+response);            
            // })
            console.log(data)
            data.forEach(element => {
                this.rows.push(element)
            });
            this.regionWiseCount()
        },
        regionWiseCount(){
            let selection = data.filter(el=>el['Customer_Region']==='North')
            console.log(selection)
            var months=[]
            console.log(selection[0]['Date of Purchase'].split('/')[0])
            for (var i=1;i<=12;i++){
                months[i-1]=selection.filter(e=>{
                    console.log("date:::::"+e['Date of Purchase'].split('/')[0]+'/////'+i.toString())
                    return i.toString()===e['Date of Purchase'].split('/')[0]
                })
            }
            console.log(months)
        },
        loadData(data){
            console.log(data)
            data.forEach(element => {
                this.rows.push(element)
            });
        },
        changeCell(changedData, column, row){
            this.rows[row][column]=changedData
        }
    }
}
</script>

<style>
</style>