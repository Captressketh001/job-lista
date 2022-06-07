<template>
<div>
 <div class="header">

 </div>
 <div class="search-bar" v-if="show==true">
     <ul class="search-results">
         <li class="filtered"  v-for="(data, ix) in filtered" :key="ix" @click="cancel(data)"> <button type="submit">{{data}}
             <!-- <span style="background:blue; padding: 5px"><img src="./assets/images/icon-remove.svg" alt="" srcset=""></span> -->
                 </button></li> 
         <li class="clear-filter" @click="clear">Clear</li>
     </ul>
 </div>
 <div class="job-content-frame" id="filtered" v-for="data in myJson" :key="data.id">
     <div class="job-content">
         <div style="" class="row-1">
             <div>
                  <img class="fir-author-image fir-clickcircle" src='./assets/images/photosnap.svg' alt="logo" >
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
                     <div class="items" v-if="data.posted_at">{{data.posted_at}}</div>
                    <div class="items" v-if="data.contract">{{data.contract}}</div>
                    <div class="items" v-if="data.location">{{data.location}}</div>
                 </div>
             </div>
         </div>
         <div class="row-2" v-if="data.languages || data.tools">
            <div v-for="(items, ix) in data.languages" :key="ix">
                <div class="item" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(items)">{{items}}</div>
            </div>
            <div v-for="(item, ix) in data.tools" :key="ix">
                <div class="item" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(item)">{{item}}</div>
            </div>
            <div v-if="data.level" style="cursor:pointer; color: hsl(180, 29%, 50%);" @click="filteredResult(data.level)">{{data.level}}</div>
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
