<script setup lang="ts">
import {computed} from 'vue'

const props = defineProps<{
    currentPage: number,
    pagesArr: number[]
}>()

const emit = defineEmits<{
    (e: 'update', value: number): void
}>()

const newArr = computed(()=>{

  if(props.pagesArr.length < 6) return props.pagesArr

    
  if(props.currentPage > 3 && props.currentPage < props.pagesArr.length-3){
  	return [...[props.pagesArr[0],'...', ...props.pagesArr.slice(props.currentPage -2,props.currentPage+2),'...', props.pagesArr[props.pagesArr.length-1]]]
  }else if(props.currentPage  <=3){
    return  [...[...props.pagesArr.slice(0,4),'...', props.pagesArr[props.pagesArr.length-1]]]
  }else{
    return	[...[props.pagesArr[0],'...', ...props.pagesArr.slice(-5)]]
  }
})


const emitValue = (page:number|string) =>{
  if(typeof page === 'number'){
    emit('update', page)
  }

}


</script>


<template>
    <ul class="pagination__counts">
        <li class="pagination__count" v-for="page in newArr" :key="page" 
            :class="{active: page === currentPage}" 
            @click="emitValue(page)"
            >{{page}}</li>
    </ul>
</template>

<style scoped>

.pagination__count{
    cursor: pointer;
    font-size: 2.8rem;
  }
  
  .pagination__count:hover{
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.774);
  }
  
  .pagination__count.active{
    font-weight: 900;
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.774);
  }
  
  
  
  .pagination__counts{
    display: flex;
    justify-content: center;
    gap: 10px;
  }

</style>