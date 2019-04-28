# navigation 改良
vue app 缓存前进刷新后退不刷新


用法:

main.js
import Navigation from './components/navigation'
Vue.use(Navigation, { router, store })

App.vue
<navigation>
    <router-view/>
</navigation>


Tabber 一直保持缓存 标志 isKeepAlive:true 如
router.js

{
    path: '/market/',
    name: 'market',
    component: (resolve) => {
      require(['./../page/market/index'], resolve)
    },
    meta: {
      isKeepAlive: true
    }
  }
  
  https://daneden.github.io/animate.css/
  结合Transition、Animate  Route过渡动画:
  
  <transition :enter-active-class="enterTransition"
                :leave-active-class="leaveTransition">
      <navigation>
        <router-view class="child-view"/>
      </navigation>
    </transition>
    
export default {
    name: 'app',
    components: {
      NavBar,
      loading, blankPage, CustomerService,DownloadtheAD
    },
    data() {
      return {
        enterTransition: 'animated fadeIn',
        leaveTransition: 'animated fadeOut'
      }
    },
    created(){
      this.setTransition()
    },
    methods: {
      setTransition () {
        this.$navigation.on('forward', (to, from) => {
          const meta = to.route.meta
          if (meta.hasOwnProperty('isKeepAlive') && meta.isKeepAlive) {
            this.enterTransition = ''
            this.leaveTransition = ''
          } else {
            this.enterTransition = 'animated fadeInRight'
            this.leaveTransition = 'animated fadeOutLeft'
          }
        })
        this.$navigation.on('back', (to, from) => {
          this.enterTransition = 'animated fadeInLeft'
          this.leaveTransition = 'animated fadeOutRight'
        })
        this.$navigation.on('replace', (to, from) => {
          this.enterTransition = 'animated fadeIn'
          this.leaveTransition = 'animated fadeOut'
        })
      }
   }
}
</script>

<style lang="scss">
.child-view {
  position: absolute;
  width:100%;
}
</style>
    
    
    
