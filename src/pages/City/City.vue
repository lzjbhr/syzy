<template>
  <div>
    <city-header></city-header>
    <!-- 往search组件里传递cities数据 -->
    <city-search :cities='cities'></city-search>
     <!-- 将axios获取的json数据cities,hotCities传递给List局部组件 -->
    <!-- 将letter参数在传递给List局部组件 -->
    <city-list :cities='cities' 
               :hot='hotCities'
               :letter='letter'
               ></city-list>
               <!-- 将axios获取的json数据citites传递给alphabet局部组件 -->
    <city-alphabet 
               :cities='cities'
               @change='handleLetterChange'
               >
                <!--监听Alphabet组件里的change事件-->
               </city-alphabet>
  </div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'
export default {
  name: 'City',
  components:{
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },

  data () {
    return {
      cities: {},
      hotCities: [],
      letter:''
    }
  },
  methods:{
    getCityInfo () {
      axios.get('/api/city.json').then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res =res.data
      if(res.ret && res.data){
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}

</script>

<style lang="stylus" scoped>

</style>

