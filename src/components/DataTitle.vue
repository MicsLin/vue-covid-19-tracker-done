<template>
    <div class="text-center">
        <h2 class="text-3xl font-bold">{{text}}</h2>
        <div class="text-2xl mt-4 mb-10">
            {{timesStamp}}
        </div>
    </div>
</template>


<script>
// 時間
import moment from 'moment'

export default {
    name:'DataTitle',
    props:[
        'text',
        'dataDate',
    ],
    computed:{
        timesStamp:function(){
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
            
        }
    }
}
</script>