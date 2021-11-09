<template>
    <div class="about">
        <h1>Hello Please add user</h1>
        <input v-model="message" v-on:input="onSubmitName"  placeholder="edit me">

        <p>Message is: {{ message }}</p>
    </div>
</template>
<script>
export default {
    name: 'UserAdd',
    data(){
        return{
            message:''
        }
    },
    methods:{
        onSubmitName(event){
            console.log(event)
            this.$emit('ontype',this.message)
        }
    }
}
</script>