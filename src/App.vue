<template>
  <v-app>
    <v-system-bar window>
      <v-icon icon="mdi-radar" class="me-2" />
      <span>VRChat Flight Radar</span>
      <v-spacer />
      <TrackingStatue/>
      
    </v-system-bar>
    <v-navigation-drawer rail expand-on-hover>
      <v-list density="compact" nav>
        <v-list-item
          v-for="item in navigationItems"
          :key="item.value"
          :title="item.title"
          :value="item.value"
          :prepend-icon="item.icon"
          @click="selectedItemValue = item.value"
          nav
        />
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <RouterView />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { RouterView } from "vue-router";
import { defineComponent } from "vue";
import TrackingStatue from './components/TrackingStatue.vue';

export default defineComponent({
  data() {
    return {
      selectedItemValue: '',
      navigationItems: [
        {
          title: "Radar",
          value: "/",
          icon: "$radar",
        },
        {
          title: "Analytics",
          value: "/analytics",
          icon: "$poll",
        },
        {
          title: "Event",
          value: "/event",
          icon: "$calendar",
        },
      ],
    };
  },
  components: {
    TrackingStatue
  },
  watch: {
    selectedItemValue(newValue, oldValue) {
      if (newValue != oldValue) this.$router.push(newValue);
    }
  },
});
</script>
