<template>
    <select v-model="selected" @change="onChange()" class="form-select mt-1 block w-full border p-3 rounded mt-10">
        <option value="0">Select Countries</option>
        <option v-for="country in countries" :value="country.ID">{{country.Country}}</option>
    </select>
</template>

<script>
export default {
    name:'CountrySelect',
    props:['countries'],
    data(){
        return{
            selected:0
        }
    },
    methods:{
        onChange(){
            const country = this.countries.find(item => item.ID === this.selected)
    
            this.$emit('get_country',country)
        }
    }
}
</script>