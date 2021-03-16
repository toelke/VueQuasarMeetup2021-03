<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="leftDrawerOpen = !leftDrawerOpen" />

        <q-toolbar-title>
          Photo App
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered content-class="bg-grey-1">
      <q-list v-for="(menuItem, index) in menuList" :key="index">
        <q-item :to="localized_url(menuItem.link)" clickable v-ripple>
          <q-item-section avatar>
            <q-icon :name="menuItem.icon" />
          </q-item-section>
          <q-item-section>
            {{ menuItem.title }}
            <q-item-label caption>{{ menuItem.caption }}</q-item-label>
          </q-item-section>
        </q-item>
        <q-separator v-if="menuItem.separator" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  components: {},
  data() {
    return {
      leftDrawerOpen: false,
      menuList: [
        {
          title: 'Upload',
          caption: 'This is to upload the files',
          icon: '',
          link: '/upload'
        },
        {
          title: 'View',
          caption: '',
          icon: 'code',
          link: '/view'
        },
        {
          title: 'Impressum',
          caption: '',
          icon: 'play_for_work',
          link: '/impressum'
        }
      ]
    };
  },
  methods: {
    localized_url(url) {
      return url;
    },
    async logout() {
      const stat = await auth_logout();
      if (stat.status == 'ok') {
        this.loggedIn = false;
      }
    }
  }
};
</script>
