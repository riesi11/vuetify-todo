<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      :mobile-breakpoint="768"
      app
    >
      <v-img
          class="pa-4 pt-7"
          src="see.jpg"
          height="170"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar size="60" class="mb-2">
          <img
              src="me.jpg"
              alt="Timo"
          >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">Timo Riesenberger</div>
        <div class="white--text text-subtitle-2 font-weight-bold">timo_riesenberger</div>
      </v-img>

      <v-list
          dense
          nav
      >
        <v-list-item
            v-for="item in items"
            :key="item.title"
            :to="item.to"
            link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
        app
        color="primary"
        dark
        shrink-on-scroll
        src="see.jpg"
        scroll-target="#scrolling-techniques-2"
        :height="$route.path === '/' ? '230' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
            v-bind="props"
            gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search></search>
        </v-row>
        <v-row>
          <v-tool-bar-title
              class="text-h4 ml-4"
          >{{ $store.state.appTitle }}
          </v-tool-bar-title>
        </v-row>
        <v-row>
          <live-date-time></live-date-time>
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task></field-add-task>
        </v-row>
      </v-container>

    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar></snackbar>
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from "@/components/Shared/Snackbar";
import Search from "@/components/Tools/Search";
import LiveDateTime from "@/components/Tools/LiveDateTime";
import FieldAddTask from "@/components/Todo/FieldAddTask";

export default {
  data: () => ({ drawer: null,
                  items: [
                    { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
                    { title: 'About', icon: 'mdi-help-box' , to: '/about'},
                  ],
  }),
  mounted() {
    this.$store.dispatch('getTasks')
  },
  components: {
    'snackbar': Snackbar,
    'search': Search,
    'live-date-time': LiveDateTime,
    'field-add-task': FieldAddTask,
  }
}
</script>

<style lang="sass">
  .header-container
    max-width: none !important
</style>