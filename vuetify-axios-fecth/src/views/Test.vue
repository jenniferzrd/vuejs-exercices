<template>
  <div>
    <h1>test</h1>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-toolbar color="teal" dark>
            <v-toolbar-side-icon></v-toolbar-side-icon>

            <v-toolbar-title>Inbox</v-toolbar-title>

            <v-spacer></v-spacer>

            <v-btn icon>
              <v-icon>search</v-icon>
            </v-btn>

            <v-btn icon>
              <v-icon>more_vert</v-icon>
            </v-btn>
          </v-toolbar>
          <v-list>
            <v-list-tile v-for="user in users" :key="user.id" >
              <v-list-tile-content :class="getColor(user.house)">
                <v-list-tile-title
                  v-if="user.house"
                  v-text="user.house"
                ></v-list-tile-title>

                <v-list-tile-title v-else v-text="text"></v-list-tile-title>
              </v-list-tile-content>

              <v-list-tile-content>
                <v-list-tile-title v-text="user.name"></v-list-tile-title>
              </v-list-tile-content>

              <v-list-tile-avatar>
                <img :src="user.image">
              </v-list-tile-avatar>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      users: [],
      text: 'No house',
      getColor(house) {
        switch (house) {
          case 'Gryffindor':
            return 'gryffindor';
          case 'Slytherin':
            return 'slytherin';
          case 'Hufflepuff':
            return 'hufflepuff';
          case 'Ravenclaw':
            return 'ravenclaw';
          default:
            return 'noHouse';
        }
      },
    };
  },
  created() {
    axios
      .get('http://hp-api.herokuapp.com/api/characters')
      .then((response) => {
        this.users = response.data;
      })
      .catch((e) => {
        /* eslint-disable no-alert, no-console */
        console.log(e);
      });
  },
};
</script>

<style>
.gryffindor {
  color: #B71C1C;
}
.hufflepuff {
  color: #C0CA33;
}
.ravenclaw {
  color: #283593;
}
.slytherin {
  color: #00E676;
}

.noHouse {
  color: #7E57C2;
}
</style>
