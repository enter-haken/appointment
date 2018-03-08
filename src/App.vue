<template>
  <div id="app">
    <div>
        <md-button class="md-raised md-primary" v-on:click="signIn">Sign in</md-button>
        <md-button class="md-raised md-primary" v-on:click="signOut">Logout</md-button>
    </div>
    <event-list :gridData="eventResult" />
  </div>
</template>

<script>
/*global gapi process */
import EventList from './components/EventList.vue'

import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'

Vue.use(VueMaterial)

const CLIENT_ID = process.env.VUE_APP_CLIENT_ID; 
const DISCOVERY_DOCS = ["https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest"];
const SCOPES = "https://www.googleapis.com/auth/calendar.readonly";

export default {
  name: 'app',
  mounted: function() {
    this.gapiLoad();
  },
  data: function() {
      return { eventResult : [] } 
  },
  components: {
    EventList 
  },
  methods: {
    // https://developers.google.com/api-client-library/javascript/samples/samples#authorizing-and-making-authorized-requests
    gapiLoad: function() {
      gapi.load('client:auth2', this.initClient)
    },
    initClient: function() {
      gapi.client.init({
      clientId: CLIENT_ID,
      discoveryDocs: DISCOVERY_DOCS,
      scope: SCOPES
      }).then(() => { 
          gapi.auth2.getAuthInstance().isSignedIn.listen(this.signedIn);
          // get signed in status on startup
          this.signedIn(gapi.auth2.getAuthInstance().isSignedIn.get());
      })
    },
    signedIn: function(isSignedIn) {
        if (isSignedIn) {
            gapi.client.calendar.events.list({
              'calendarId': 'primary',
              'timeMin': (new Date()).toISOString(),
              'showDeleted': false,
              'singleEvents': true,
              'maxResults': 10,
              'orderBy': 'startTime'
            }).then((response) => {
              this.eventResult = response.result.items;
            })  
        } else {
            this.eventResult = []; 
        }
    },
    signIn: function() {
      gapi.auth2.getAuthInstance().signIn();
    },
    signOut: function() {
      gapi.auth2.getAuthInstance().signOut();
    }
  }
}
</script>
