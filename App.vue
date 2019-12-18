<template>
  <app-navigator></app-navigator>
</template>

<script>
import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";

// registering all native-base components to the global scope of the Vue
Vue.use(VueNativeBase);

import { createAppContainer, createStackNavigator } from "vue-native-router";
import HomeScreen from "./screens/HomeScreen.vue";
import DetailsScreen from "./screens/DetailsScreen.vue";
import Report from "./screens/Report.vue";
import About from "./screens/About.vue";
import Chart from "./screens/Chart.vue";
const StackNavigator = createStackNavigator(
  {
    Home: {
      screen: HomeScreen,
      navigationOptions: {
        title: "Login",
        header: null
      }
    },
    Report: {
      screen: Report,
      navigationOptions: {
        title: "REPORT DATA BUSDEV",
        header: null
      }
    },
    About: {
      screen: About,
      navigationOptions: {
        title: "REPORT DATA BUSDEV",
        header: null
      }
    },
    Details: {
      screen: DetailsScreen,
      navigationOptions: {
        title: "REPORT DATA BUSDEV",
        header: null
      }
    },
    Chart: {
      screen: Chart,
      navigationOptions: {
        title: "REPORT DATA BUSDEV",
        header: null
      }
    }
  },
  {
    // initialRouteName: "Home"
  }
);
const AppNavigator = createAppContainer(StackNavigator);
export default {
  components: { AppNavigator }
};
</script>