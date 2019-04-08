<template>
  <section class="container">
    <input type="text" v-model="zipcode" />
    <button @click="searchAddressInfo()">検索</button>
    {{message}}
    {{zipcode}}
    {{addressData}}
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
        this.addressData = res.data.results;
      }).catch((error) => {
        this.message = 'error'
      })
    }
  }
}

</script>

<style>

</style>
