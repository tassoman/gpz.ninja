<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-positive text-dark">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> GPZ Ninja Homepage </q-toolbar-title>

        <div>
          <q-toggle
            color="dark"
            checked-icon="dark_mode"
            unchecked-icon="light_mode"
            ref="darkMode"
            v-model="$q.dark.isActive"
            @update:model-value="toggleDark"
          />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Essential Links </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import EssentialLink from 'components/EssentialLink.vue';
import { useQuasar } from 'quasar';

const linksList = [
  {
    title: 'GitHub repository',
    caption: 'Public repository hosting website code',
    icon: 'code',
    link: 'https://github.com/tassoman/gpz.ninja',
  },
];

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
  },

  setup() {
    const $q = useQuasar();
    const leftDrawerOpen = ref(false);
    const darkMode = ref('darkMode');

    return {
      $q,
      darkMode,
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      toggleDark(v) {
        $q.dark.set(v);
      },
    };
  },
});
</script>
