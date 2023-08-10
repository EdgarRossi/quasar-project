<template>
  <q-layout view="lHh Lpr lff">
    <q-header elevated class="bg-cyan-8">
      <q-toolbar>
        <q-toolbar-title>Header</q-toolbar-title>
        <q-btn
          flat
          @click="drawer = !drawer"
          round
          dense
          icon="las la-chevron-circle-down"
        />
      </q-toolbar>
    </q-header>

    <q-drawer v-model="drawer" show-if-above :width="200" :breakpoint="400">
      <q-scroll-area
        style="
          height: calc(100% - 150px);
          margin-top: 150px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <q-item clickable v-ripple to="/" active-class="my-menu-link" exact>
            <q-item-section avatar>
              <q-icon name="las la-voicemail" />
            </q-item-section>

            <q-item-section> Inbox </q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/about" active-class="my-menu-link">
            <q-item-section avatar>
              <q-icon name="las la-star" />
            </q-item-section>

            <q-item-section> About </q-item-section>
          </q-item>

          <q-item clickable v-ripple to="/form" active-class="my-menu-link">
            <q-item-section avatar>
              <q-icon name="las la-star" />
            </q-item-section>

            <q-item-section> Form </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img
        class="absolute-top"
        src="https://cdn.quasar.dev/img/material.png"
        style="height: 150px"
      >
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
          </q-avatar>
          <div class="text-weight-bold">Razvan Stoenescu</div>
          <div>@rstoenescu</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <router-view></router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const drawer = ref(false);

    return {
      drawer,
    };
  },
};
</script>

<style lang="scss">
.my-menu-link {
  color: white;
  background: #f2c037;
}
</style>
