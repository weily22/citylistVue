<template>
  <div class="city">
    <group title="城市选择">
      <cell class="blueTitle" :title="CITY+' GPS'"></cell>
    </group>
    <ul class="abcBar"><li v-for="k in ABC" @click="scrollTo(k)" :class="k===activeK?'active':''">{{k}}</li></ul>
    <div class="cityBody" @scroll="scrollback">
      <group :title="item" v-for="item in ABC" class="ABCitem" :id="item">
        <ul v-for="j in list" v-if="j.code.charAt(0)===item">
          <li @click="CCity(j.name)">{{j.name}}</li>
        </ul>
      </group>
    </div>
  </div>
</template>
<script>
import {Group, Cell} from 'vux'
import CityList from './city.json'
export default {
  components: {
    Group,
    Cell
  },
  data () {
    return {
      ABC: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
      CITY: '上海',
      activeK: 'A',
      list: CityList
    }
  },
  methods: {
    scrollTo (index) {
      this.activeK = index
      let pos = document.getElementById(index)
      let citybar = document.getElementsByClassName('cityBody')[0]
      citybar.scrollTop = pos.offsetTop
    },
    scrollback () {
      let citybar = document.getElementsByClassName('cityBody')[0]
      let items = document.getElementsByClassName('ABCitem')
      let arr = Array.from(items)
      for (let k of arr) {
        if (k.offsetTop <= citybar.scrollTop) {
          this.activeK = k.id
        }
      }
    },
    CCity (name) {
      this.CITY = name
      console.log(`我选择了${name}`)
    }
  }
}
</script>
<style lang="less" scoped>
  .city{
    position: absolute;
    top:0;
    bottom:0;
    width:100%;
    overflow: hidden;
    .blueTitle{
      color:#2196f3;
    }
    .abcBar{
      position: absolute;
      right:0;
      z-index:100;
      top:80px;
      height:80%;
      width:30px;
      text-align: center;
      overflow: auto;
      font-size: 80%;
      color:#666;
      li.active{
        color:#f00;
      }
    }
    .cityBody{
      position: absolute;
      top:80px;
      bottom:0;
      width:100%;
      overflow: auto;
      li{
        padding:10px 15px;
      }
    }
  }
</style>
