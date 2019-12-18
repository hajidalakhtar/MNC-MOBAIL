<template>
<view class="container" :style="{backgroundColor:'#E6F7D5',height:1000}">
      <image
      class="center"
      :style="{width: 120, height: 120,marginTop:50 }"
      :source="{uri: 'https://avatars1.githubusercontent.com/u/27917329?s=400&u=c66e45903a40f9499d2dc98b0494049ab7c26aea&v=4'}"
    />

    <text :style="{marginTop:20,fontSize:20}">Muhammad Hajid Al Akhtar</text>
    <text :style="{fontSize:15}">XII RPL 1</text>
      <image
      class="center"
      :style="{width: 250, height: 250,marginTop:-3 }"
          :source="require('../assets/bg.png')"

    />
    <view :style="{flex: 1, flexDirection: 'row',marginTop:10}">
    <nb-button iconLeft light :style="{width:130}" :onPress="GoGithub">
      <image
      class="center"
      :style="{width: 30, height: 30,marginTop:-3 }"
          :source="require('../assets/githublogo.png')"

    />
        <text :style="{paddingRight:30}">GITHUB</text>
    </nb-button>

    <nb-button iconLeft :style="{width:130,marginLeft:10}" :onPress="GoWeb">
        <nb-icon active name="home" :style="{color:'white'}" />
        
        <text :style="{paddingRight:30,color:'white'}">WEB</text>
    </nb-button>
    </view>

     
</view>
     
      
     
</template>

<script>
import { Linking } from 'expo';
export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    goToHomeScreen() {
      this.navigation.navigate("Home");
    }, 
     GoGithub(){
      Linking.openURL('https://github.com/hajidalakhtar')
  },
    GoWeb(){
        Linking.openURL('https://ajiporto.com/')
    },
  }

}
</script>
<style>
.container {
  align-items: center;
  justify-content: center;
}

.center {
  margin-top: 10px;
  /* display: block; */
  margin-left: auto;
  margin-right: auto;
  /* width: 50%; */
}
.contanier {
  /* display: block; */
  margin-left: auto;
  margin-right: auto;
  width: 90%;
  /* height: 200px; */
}
</style>