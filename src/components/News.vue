<template>
        <div  class="grid grid-cols-1 md:grid-cols-2  lg:grid-cols-3 gap-x-10  xl:gap-x-20 mt-4">
            <div v-for="newCompo in news" :key="newCompo.id">
                <NewsItem :data="newCompo"  />
            
            

            </div>
        </div>
</template>

<script>

import NewsItem from "./NewsItem.vue";

export default {
  name: "News",
  components:{
      NewsItem
  },
  props: {
    news: {
      type: Array,
      required: true,
    },
  },
};
</script>