<template>
    <div>
        <md-table v-model="gridData" md-card>
            <md-table-toolbar>
                <h1 class="md-title">Events</h1>
            </md-table-toolbar>

            <md-table-row slot="md-table-row" slot-scope="{ item }">
                <md-table-cell md-label="Start">{{ item.start.dateTime | moment }}</md-table-cell>
                <md-table-cell md-label="End">{{ item.end.dateTime | moment }}</md-table-cell>
                <md-table-cell md-label="Created">{{ item.created | moment }}</md-table-cell>
                <md-table-cell md-label="Summary"><a :href="item.htmlLink" target="_blank">{{ item.summary }}</a></md-table-cell>
                <md-table-cell md-label="Creator">{{ item.creator.displayName }}</md-table-cell>
                <md-table-cell md-label="Organizer">{{ item.organizer.displayName }}</md-table-cell>
           </md-table-row>
        </md-table>
    </div>
</template>


<script>

import moment from 'moment'

export default {
  props: {
      gridData: {
        default: () => { return [] },
        type: Array
      }
  },
  methods: {
    moment: function () {
      return moment();
    }
  },
  filters: {
    moment: function (date) {
      if (date) {
        return moment(date).locale('en').format('lll');
      }
      return '';
    }
  },
  name: 'event-list'
}
</script>
