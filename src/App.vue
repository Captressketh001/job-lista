<template>
<div>
 <div class="header">

 </div>
 <div class="search-bar" v-show="filtered.length > 0">
     <ul class="search-results">
         <li class="filtered"  v-for="(data, ix) in filtered" :key="ix" @click="cancel(data)"> <button type="submit">{{data}}
             <!-- <span style="background:blue; padding: 5px"><img src="./assets/images/icon-remove.svg" alt="" srcset=""></span> -->
                 </button></li> 
         <li class="clear-filter" @click="clear">Clear</li>
     </ul>
 </div>
 <div class="job-content-frame" id="filtered" v-for="data in filteredJobs" :key="data.id">
     <div class="job-content">
         <div style="" class="row-1">
             <div>
                  <img class="fir-author-image fir-clickcircle" :src='data.logo' alt="logo" >
             </div>
             <div class="job-description">
                 <div style="display: flex;padding-bottom: 10px; flex-wrap:wrap">
                     <div class="items">{{data.company}}</div>
                    <div class="items" v-if="data.new">NEW!</div>
                    <div class="items" v-if="data.featured">FEATURED</div>
                 </div>
                 <div style="display: flex; padding-bottom: 10px;">
                     <div class="fig-author-figure-title">{{data.position}}</div>
                 </div>
                 <div style="display: flex;">
                     <span class="items" v-if="data.postedAt">{{data.postedAt}}</span>
                     <span>&bull;</span>
                    <span class="items" v-if="data.contract">{{data.contract}}</span>
                    <span>&bull;</span>
                    <span class="items" v-if="data.location">{{data.location}}</span>
                 </div>
             </div>
         </div>
         <div class="row-2">
            <div v-for="(items, ix) in data.languages" :key="ix">
                <div class="item" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(items)">{{items}}</div>
            </div>
            <div v-for="(item, ix) in data.tools" :key="ix">
                <div class="item" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(item)">{{item}}</div>
            </div>
            <div v-if="data.level" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(data.level)">{{data.level}}</div>
            <!-- <div v-for="category in filtering" :key="category" class="item" @click="filteredResult(category)">{{category}}</div> -->
         </div>
        </div>
 </div>
</div>
</template>

<script>
import json from './data.json'
export default {
  data (){
      return{
          myJson: json,
          filtered: [],
          show: false
      }

  },
  computed:{
      filtering(){
        // let categories = ''
         let cat = ''
          let data = this.myJson
          for(let p=0; p < data.length; p++){
             cat = [data[p].role, data[p].level, data[p].languages, data[p].tools].flat()
          }
        //   data.forEach(i => {
        //     categories = [i.role, i.level, i.languages, i.tools].flat()
        // })
        console.log('cat')
        console.log(cat)
        //   return categories
        return cat
      },
      filteredJobs(){
          let x = this.myJson
          if(this.filtered.length === 0){
              return x
          }
          return x.filter(job => {
              let match = true
              const jobCategories = [job.languages, job.role, job.level, job.tools].flat()
              this.filtered.forEach(categorie => {
                  match = match && (jobCategories.indexOf(categorie) >= 0)
              })
              return match
          })
      }
        //  return jobs.value.filter(job => {
        // let match = true
        // const jobCategories = [job.languages, job.role, job.level, job.tools].flat()
        // categoriesToFilter.value.forEach(categorie => {
        //   match = match && (jobCategories.indexOf(categorie) >= 0)
        // })
        // return match
    //   data.forEach((i, index) => {
          
    //   })
    //   const categories = computed(() => [props.job.role, props.job.level, props.job.languages, props.job.tools].flat())
  },
  methods: {
      filteredResult(data){
          console.log(data)
            if (this.filtered.includes(data)) {
                console.log('isee',data);
                this.show = true;
                
                
                // var index = this.filtered.indexOf(data);
                // this.filtered.splice(index, 1);
                // console.log(this.filtered.splice(index, 1))
                // console.log('I am index:' + index)
            } else {
            this.filtered.push(data);
            // let filtering = document.getElementById('filtered')
            //     let tr = filtering.getElementsByClassName('job-content')
            //      for (let i=0; i<tr.length; i++){
            //           let td = tr[i].getElementsByClassName("item")[0];
            //           if(td){
            //               let text = td.innerText || td.textContent;
            //               console.log('I am text')
            //               console.log(text)
            //               if (text.toUpperCase().indexOf(data) > -1) {
            //                     tr[i].style.display = "block";
            //                     filtering.style.display = "flex";
            //                 } else {
            //                     tr[i].style.display = "none";
            //                     filtering.style.display = "block";
            //                 }
                          
            //             }
            //     }
            this.show = true;
            console.log(this.filtered)
            }
        
      },
      cancel(data){
          if (this.filtered.includes(data)) {
                console.log('isee',data);
                var index = this.filtered.indexOf(data);
                this.filtered.splice(index, 0);
                console.log(this.filtered.splice(index, 1))
                console.log('I am index:' + index)
            }
      },
      clear(){
          this.filtered = []
          this.show = false
      }
    }
}
</script>

<style>

</style>
