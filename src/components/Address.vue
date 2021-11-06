<template>
  <div>
    <section class="container">
      <input type="text" placeholder="郵便番号を入力" v-model="zipcode"/>
      <button @click="onClick()">住所自動入力</button>
      <!-- <p>{{resultData}}</p> -->
      <!-- <p>都道府県：</p>
      <p>住所1：</p>
      <p>住所2：</p> -->
      <p v-if="zipcode.length < 6">郵便番号を入力してください</p>
      <p v-else>{{address["results"]}}</p>
    </section>
  </div>
  
</template>

<script>
export default {
  data:function(){
    return{
      zipcode:'',
      address:''
    }
  },
  methods:{
    onClick(){
        fetch('https://zip-cloud.appspot.com/api/search?zipcode='+this.zipcode)
        .then(response => {
        return response.json();
      })
       .then(data => { 
        this.address = data;
        console.log(data);

    })
    }
  }
}
</script>