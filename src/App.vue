<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-card class="mx-auto" max-width="400">
        <v-list>
          <v-list-item-group v-model="model" mandatory color="indigo">
            <v-list-item v-for="(item, i) in items" :key="i" :to="item.url">
              <v-list-item-icon>
                <v-icon v-text="item.icon"></v-icon>
              </v-list-item-icon>

              <v-list-item-content>
                <v-list-item-title v-text="item.text"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Mister Admin</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({ drawer: null,
   items: [
        {
          icon: 'mdi-home',
          text: 'Home',
          url: '/'
        },
        {
          icon: 'mdi-account',
          text: 'Leads',
          url: '/leads'
        },
      
       
      ],
      model: 1,
  }),
};
</script>