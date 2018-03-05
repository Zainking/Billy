<template>
  <div id="app">
    <h1>比利·海灵顿</h1>
    <h2>Billy Herrington</h2>
    <div class="Billy"><img src="http://ov4zgil7v.bkt.clouddn.com/Billy.jpg" alt="Billy"></div>
    <p>比利海灵顿生于1969年7月14日，是美国知名㚻片（GV）演员之一，早年由于在他拍过的GV当中有许多莫名其妙的摔跤戏，又在途中发出许多奇奇怪怪的声音，因此自然就成为Nico动画上面的好素材。</p>
    <p>比利海灵顿因为其视频素材的广泛流行，很快被中日宅圈内的网友熟知，日本网友因其健硕的身材称其为“ANIKI”（兄贵，大哥的意思），或“森の妖精”，随后比利的事迹与视频传入A站并影响至今。</p>     
    <p>作为A/B站鬼畜区史诗级素材主演之一，与哲♂学文化的发起者之一，比利海灵顿深受国内外二次元网友的喜爱，国内粉丝一般称其为王♂。</p>
    <p>比利海灵顿于2018年3月3日在一场车祸中去世，年仅48岁。比利海灵顿的母亲与导演分别占在FB与推特上确认了其去世的消息。英文维基百科也随后更新了比利海灵顿词条的生卒年月。</p>
    <div><a href="#" class="btn" @click="onCandle">{{isCandled ? '你已经点蜡' : isCandleing ? '正在点蜡...' : '🕯️为王点蜡'}}</a></div>
    <h2 class='title'>共有<span class="candleNum">{{candleNum}}</span>人为他献上了蜡烛</h2>
    <p class="candles"><span v-for="n in candleNum">🕯️</span></p>
  </div>
</template>

<script>
import $ from 'jquery'
export default {
  name: 'app',
  data () {
    return {
      candleNum: 0,
      isCandled: false,
      isCandleing: false,
    }
  },
  methods: {
    onCandle (e) {
      e.preventDefault()
      if (this.isCandleing || this.isCandled) {
        return false;
      }
      this.isCandleing = true
      $.post('http://wzy88665.gotoip55.com/billyApi/billyApi.php', (data) => {
        data = JSON.parse(data)
        if (data) {
          this.isCandled = true
          this.candleNum++
          window.localStorage.setItem('isCandled', true)
        }
        this.isCandleing = false
      })
    }
  },
  created () {
    $.get('http://wzy88665.gotoip55.com/billyApi/billyApi.php', (data) => {
      data = JSON.parse(data)[0]
      this.candleNum = parseInt(data)
      console.log(this)
    })
    if (window.localStorage.getItem("isCandled")) {
      this.isCandled = true
    }
  }
}
</script>

<style>
body {
  background-color: #000;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #888;
  margin: 60px auto;
  background-color: #000;
  max-width: 600px;
  width: 100%;
}
.Billy {
  width: 100%;
  max-width: 395px;
  display: block;
  margin: 0 auto;
}
h1, h2 {
  font-weight: normal;
}
p {
  text-indent: 2em;
  text-align: left;
}
.btn {
  color: #333;
  font-size: 1.5em;
  background-color: #aaa;
  text-decoration: none;
  box-sizing: border-box;
  border: 1px solid #888;
  padding: 10px 20px;
  border-radius: 5px;
}
.btn:hover {
  background-color: #888;
  border-color: #aaa;
}
.title {
  border-bottom: 1px solid;
  text-align: left;
  margin-top: 60px;
}
.candleNum {
  color: #fff;
}
.candles {
  font-size: 2em;
  text-indent: 0;
}
</style>
