<template>
  <div class="pa-2">
    <div class="text-h4">Focus</div>
    <v-divider class="mb-2"></v-divider>
    <div class="text-h6">{{focus.status}}</div>
    <div v-if="focus.hfr">
      <v-row no-gutters>
        <v-col>
          HFR:
        </v-col>
        <v-col>
          {{focus.hfr.toFixed(2)}}
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col>
          Position:
        </v-col>
        <v-col>
          {{focus.pos}}
        </v-col>
      </v-row>
    </div>
    <LastNotification />
    <v-divider class="mb-2"></v-divider>
    <v-list>
      <v-list-item>
        <v-btn block @click="toggleFocus">{{startStopText}}</v-btn>
      </v-list-item>
      <v-list-item>
        <v-btn block @click="focusReset">Reset</v-btn>
      </v-list-item>
    </v-list>
  </div>
</template>
<script>
import { mapState, mapActions } from "vuex";
import LastNotification from "@/components/common/LastNotification"

export default {
  components: {
    LastNotification,
  },
  computed: {
    ...mapState([
      'focus',
    ]),
    startStopText() {
      if (this.focus.status === 'In Progress') {
        return "Stop Autofocus";
      }

      return "Start Autofocus";
    }
  },
  methods: {
    ...mapActions([
      'focusStop',
      'focusStart',
      'focusReset',
    ]),
    toggleFocus() {
      if (this.startStopText === "Start Autofocus") {
        this.focusStart();
      } else {
        this.focusStop();
      }
    },
  },
};
</script>
