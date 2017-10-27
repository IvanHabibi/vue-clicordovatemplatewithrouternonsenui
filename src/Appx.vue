<template>
<div>

  <button @click="wlCommonInit">asd</button>
  <div>
    {{test}}
    {{wl}}
    {{url}}
    {{datawl}}
  </div>
</div>
</template>

<script>
import HomePage from './components/HomePage'
import MenuPage from './components/MenuPage'


export default {
  name: 'app',
  data() {
    return {
      datawl: '',
      url:'',
      wl:'',
      test:''

    }
  },
  computed: {
    menuIsOpen: {
      get() {
        return this.$store.state.splitter.open
      },
      set(newValue) {
        this.$store.commit('splitter/toggle', newValue)
      }
    }
  },
  components: {
    HomePage,
    MenuPage
  },
  methods: {
    wlCommonInit() {
      let self = this
      this.test = 'test'
      var serverUrl = WL.App.getServerUrl(function(success){
        self.url = success;
    console.log(success);
}, function(fail){
  self.url = fail;
    console.log(fail);
});
self.wl = serverUrl
      // WL.App.getServerUrl(function (url) {
      //   this.url = url;
      // });
      console.log('ini wlauth',WLAuthorizationManager)
      let token = WLAuthorizationManager.obtainAccessToken()
        .then(
          function(accessToken) {
            self.datawl = `yeay connect, token nya : ${accessToken}`
            console.log(self.datawl)
          },
          function(error) {
            self.datawl = `bah error, errornya nya : ${error}`
            console.log(self.datawl)
          }
        )
        console.log('ini toket',token)
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ons-splitter-side[side=left][animation=overlay] {
  border-right: 1px solid #BBB;
}
</style>
