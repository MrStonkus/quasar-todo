<template>
  <q-layout view="hHh lpr fFf">
    <q-header reveal elevated class="bg-primary text-white">
      <q-toolbar class="row justify-end">
        

        <q-btn
          v-if="!$q.platform.is.mobile"
          dense
          flat
          round
          icon="settings"
          @click="rightDrawerOpen = !rightDrawerOpen" />
      </q-toolbar>

      <div class="q-px-lg q-pt-xl q-mb-md">
        
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{todaysDate}}</div>
      </div>
      <q-img 
        src="../statics/goldwing3.jpg"
        class="header-image absolute-top" />

    </q-header>

    <q-drawer 
      v-model="rightDrawerOpen" 
      side="right"
      behavior="mobile" 
      overlay bordered
      :breakpoint="600"
      :width="200"
      >
      <!-- drawer content -->
      <div class="q-px-lg q-pt-lg ">
        <q-avatar size="56px" class="q-mb-sm q-px-xl">
          <img src="../statics/valdas.jpg">
        </q-avatar>
        <div class="text-weight-bold">Razvan Stoenescu</div>
          <div class="">@rstoenescu</div>
      </div>

      <div>
        <q-item 
              to="/"
              exact
              clickable
              v-ripple>
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>
          <q-item-section>
            Todo
          </q-item-section>
        </q-item>

        <q-item 
              to="/help"
              exact
              clickable
              v-ripple>
          <q-item-section avatar>
            <q-icon name="help" />
          </q-item-section>
          <q-item-section>
            Help
          </q-item-section>
        </q-item>
      </div>
    </q-drawer>


    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer reveal bordered class="bg-grey-8 text-white">
      <q-toolbar 
        class="row justify-end"
        
        >
        <q-btn 
          v-if="$q.platform.is.mobile"
          flat
          dense
          round
          icon="settings"
          aria-label="Menu"
          @click="rightDrawerOpen = !rightDrawerOpen"
        />
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>










<script>
import EssentialLink from 'components/EssentialLink.vue'
import { date } from 'quasar'



export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      rightDrawerOpen: false,
    }
  },
  computed: {
    todaysDate(){
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd D MMMM')
    }
  }
}
</script>

<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.5;
    filter: grayscale(100%)
  }
</style>