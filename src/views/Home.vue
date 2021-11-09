<template>
  <div class="home">
    <VueGoodTable />
  </div>
</template>

<script>
// @ is an alias to /src
import VueGoodTable from '../components/TableComponent.vue'
export default {
  name: 'Home',
  data(){
    return{
      userName:''
    }
  },
  components: {
    VueGoodTable
  },
  methods:{
    onChildType(value){
      console.log(value)
      this.userName=value
    }
  }
}
</script>
