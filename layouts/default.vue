<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>


    <!-- Footer -->
    <v-bottom-navigation
    horizontal
    height="10vh"
    fixed
    color="primary"
    app
    >
      <v-app-bar-nav-icon
      @click.stop="drawer = !drawer"
      v-ripple="false"
      plain
      />
        <v-btn v-for="(item, i) in bottomMenu" 
        :key="i"
        :to="item.to"
        v-ripple="false"
        plain>
        <span>{{ item.title }}</span>
        <v-icon>{{ item.icon }}</v-icon>
        </v-btn>
        <v-spacer/>
    </v-bottom-navigation>


  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      drawer: false,
      items: [
        {
          icon: 'mdi-account',
          title: 'Account',
          to: '/account'
        },
        {
          icon: 'mdi-bell',
          title: 'Notification',
          to: '/notification'
        }
      ],
      bottomMenu: [
        {
          icon: 'mdi-application',
          title: 'Application',
          to: '/'
        },
      ],
    }
  }
}
</script>
