<template>
    <div class=" w-full flex  customBorder bg-gray-200 overflow-x-hidden">
       <div class="flex w-1/3 text-sm sm:text-base  md:w-1/6 z-50 items-center justify-center customBgColor py-1 px-6 text-white font-bold">Top News</div>
       <div class="w-2/3 md:w-5/6 flex items-center">
       <div  class="font-light highlights  ">
            <ul class="flex items-center">
                <li v-for="topNew in topNews" :key="topNew.title">
                    <p class="flex items-center">
                        <span class="customBgColor text-white font-bold px-2">{{formatDate(topNew.publishedAt)}}</span>
                        <a target="_blank"  class="w-96 overflow-x-hidden ml-2 text-sm hover:underline hover:text-black" :href="topNew.url">{{topNew.title.substring(0,50)}}</a>
                    </p>
                </li>
            </ul>
       </div>
       </div>
      
    </div>
</template>


<script>
import axios from "axios";

export default {
    name:"BreakingNews",
    data(){
        return {
            topNews:[],
            totalResults:null,
        }
    },mounted(){

        axios.get(`${this.$store.state.baseUrl}/news/topHeadlines`).then((res)=>{
            
            this.topNews=res.data.news;
            this.totalResults=res.data.totalResults;
            
        }).catch((err)=>console.log(err))
    },methods: {
        formatDate(dateInUtcFormat){
            return new Date(dateInUtcFormat).getDate()+"/"+new Date(dateInUtcFormat).getMonth()+"/"+new Date(dateInUtcFormat).getFullYear();
        }
    },
    
}
</script>

<style>
.highlights{
   
    animation:scroll 100s infinite linear;
    
}
.customBgColor{
    background-color:#D40850;
}
.customBorder{
    border-top:3px solid #D40850;
}

@keyframes scroll{
    0%{
        transform:translateX(0);
    }
    100%{
        transform:translateX(-100%);
    }
}
</style>