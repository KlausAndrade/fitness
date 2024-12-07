<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title>
          Fitness tracker
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item>
          <q-item-section avatar>
            <q-icon :name="isDark ? 'dark_mode' : 'light_mode'" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Theme</q-item-label>
          </q-item-section>
          <q-item-section side>
            <q-toggle v-model="isDark" @update:model-value="toggleTheme" dense />
          </q-item-section>
        </q-item>

        <EssentialLink v-for="link in linksList" :key="link.title" v-bind="link" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'
import { useQuasar } from 'quasar';

const $q = useQuasar()

const linksList = [
  {
    title: 'Home',
    caption: 'Your home',
    icon: 'house',
    link: '/home'
  },
  {
    title: 'Workout',
    caption: 'Your workouts overview',
    icon: 'fitness_center',
    link: 'workout'
  },
  {
    title: 'Profile',
    caption: 'Check your statistics',
    icon: 'person',
    link: '/profile'
  },
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function toggleTheme() {
  $q.dark.toggle();
}
</script>
