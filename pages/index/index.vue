<template>
  <view >
    <song-data-picker  :localdata="items1" popup-title="请选择班级" :openSearch="true" @change="onchange1" @nodeclick="onnodeclick"></song-data-picker>
  <button @click="inp()">Click</button>
    <song-data-picker  :localdata="items2" popup-title="请选择班级" :openSearch="true" @change="onchange2" @nodeclick="onnodeclick"></song-data-picker>
    
	
	<uni-number-box @change="bindChange" v-model = "vModelValue"></uni-number-box>
	<button @click="calc()">CAL</button>
	The Rate is {{rate}},about {{result}}
  </view>
</template>

<script>
  import lxcCount from '@/components/lxc-count/lxc-count.vue'
  export default {
	  components:{
	          lxcCount
	      },
	  onLoad () {
	  /*	const _this=this
		      this.$axios.defaults.withCredentials = false;
	          this.$axios
	            .get('https://www.cbr-xml-daily.ru/daily_json.js')
	            .then(response => (this.datalist = response.data.Valute))
	            .catch(function (error) {
	              console.log(error);
				});
	  */		
	    
	    
	    
		uni.request({
		                    url: "https://www.cbr-xml-daily.ru/daily_json.js",                  
		                    method: 'get',
		                    dataType: 'json',
		                    success: (res) => {
		                        console.log(res.data.Valute);
								this.datalist = res.data.Valute
		                        // this.productList = res.data;
		                    },                  
		                });
		
		
	  	 },
	  onReady(){
		
	  },
    data() {
      return {
		vModelValue:'',
		result:'',
		datalist:{},
		
		value1:'',
		value2:'',
		rate:'',
        items1: [{
                  text: "AUD",
                  value: "53.0996",
				  text1: "AUD1",
                },
                {
                  text: "AZN",
                  value: "42.7076",
				  text1: "AZN1",
                },
                {
                  text: "GBP",
                  value: "100.1621",
				  text1: "GBP1",
                }],
		items2: [{
		          text: "AUD",
		          value: "53.0996",
				  text1: "AUD1",
		        },
		        {
		          text: "AZN",
		          value: "42.7076",
				  text1: "AZN1",
		        },
		        {
		          text: "GBP",
		          value: "100.1621",
				  text1: "GBP1",
		        }]
      }
    },
    methods: {
		
      onchange1(e) {
		
        const value = e.detail.value;
		console.log(value[0].value);
		this.value1=value[0].value;
		
      },
	  onchange2(e) {
	    const value = e.detail.value;
	  	console.log(value[0].value);
		this.value2=value[0].value;
	  },
      onnodeclick(node) {
		  
      },
	  
	  inp:function(){
		  var arr=[];
		  for(let i in this.datalist){
		  let o={text:i,value:this.datalist[i].Value};
		  arr.push(o);
		  };
		  this.items1=arr;
		  this.items2=arr;
		  console.log(arr);
		  console.log(this.items);
		  
	  },
	  oup(){
		  
		  
		  
		  
	  },
	  calc(){
		  this.rate=this.value1/this.value2;
		  this.result=this.vModelValue*this.rate;
	  },
    }
  }
</script>