<template>
  <section class="container">
    <p>{{message}}</p>
    <input type="text" v-model="zipcode" @focus="focus"/>
    <button @click="searchAddressInfo()">住所自動入力</button>
      <p>郵便番号：{{zipcode}}</p>
      <p>都道府県：{{addressData['address1']}}</p>
      <p>住所1：{{addressData['address2']}}</p>
      <p>住所2：{{addressData['address3']}}</p>
  </section>
</template>

<script>
const axios = require('axios');

let url = 'http://zipcloud.ibsnet.co.jp/api/search?zipcode=';

export default {
  data() {
    return {
      zipcode: '',
      addressData: {},
      message: ''
    }  
  },
  // async asyncData() {
    // let zipcode = '113-0024';
    // let result = await axios.get(url + zipcode);
    // return {resultData: result.data.results};
  // },
  methods: {
    searchAddressInfo: function() {
      axios.get(url + this.zipcode).then((res) => {
        if(res.data.results == null) {
          this.message = 'no data'
          return;
        }
        this.addressData = res.data.results[0];
      }).catch((error) => {
        this.message = 'error'
      })
    },
    focus: function() {
      this.zipcode = ''
      this.addressData = {}
      this.message = ''
    }
  }
}

</script>

<style>
.container {
  margin: 100px;
}
</style>
