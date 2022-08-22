<template>
  <div id="app">
    <synaps-verify
      sessionId="4fd1d553-3e5249ca-508d569c-1c6bef5e"
      :color="{ primary: '212b39', secondary: 'ffffff' }"
      lang="en"
      service="individual"
      :withFinishButton="true"
      @ready="print('ready')"
      @finish="print('finish')"
    />
  </div>
</template>

<script>
import SynapsVerify from "./components/SynapsVerify.vue";

export default {
  name: "App",
  components: {
    SynapsVerify,
  },
  methods: {
    print(data) {
      console.log(data);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
