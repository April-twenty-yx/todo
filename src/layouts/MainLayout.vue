<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
      <div class="q-pt-md q-px-md q-my-sm">
        <div class="text-h4">
          Todo
        </div>
        <div class="text-weight-thin">
          {{ today }}
        </div>
      </div>
      <q-img src="~assets/mountains.jpg" class="full-height absolute-top header-img"/>
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="220"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 142.8px); margin-top: 142.8px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item clickable v-ripple to="/" exact>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>
              <q-item-section>
                Todo
              </q-item-section>
            </q-item>
            <q-item clickable v-ripple to="/help" exact>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>
              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="~assets/mountains.jpg" style="height: 142.8px">
          <div class="absolute-center bg-transparent text-center">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="~assets/星空.jpg">
            </q-avatar>
            <div class="text-weight-bold">April twenty</div>
            <div class="text-no-wrap">@April twenty</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false
    }
  },
  computed: {
    today () {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'dddd MMMM YYYY')
    }
  }
}
</script>

<style lang="stylus">
  .header-img
    z-index -1
    opacity .5
    filter grayscale(100%)
</style>
