<template>
  <b-container class="content-container">
    <Search v-model="search" />
    <b-row>
      <b-col v-if="!filteredTeam.length">
        <p>No teams found with that name...please search again.</p>
      </b-col>
      <b-col v-else class="team-container" cols="4" v-for="(team, index) in filteredTeam" :key="index">
        <b-card class="team-card">
          <h6>{{ team.team.city }} {{team.team.name}}</h6>
          <p>Wins: {{ team.stats.standings.wins }}</p>
          <p>Losses: {{ team.stats.standings.losses }}</p>
         <p> Rank: {{ team.overallRank.rank}}</p>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import Search from './Search'
import getStats from '../services/getStats.js'
export default {
  name: "Stats",
  data() {
    return {
      teams: [],
      input: '',
      error: false,
      search: ''
    };
  },
  components: {
    Search
  },
  created() {
    getStats.getDynamicScores().then(response => {
      this.teams = response.data.teams
      console.log(this.teams)
    })
  },
  computed: {
    filteredTeam() {
      return this.teams.filter(team => {
        let teamName = `${team.team.city} ${team.team.name}`
        return teamName.toLowerCase().includes(this.search.toLowerCase())

      });
    }
  }
};
</script>

<style>
.content-container {
  margin: 2% auto;
}
.team-container {
  margin-bottom: 2%;
  text-align: center;
}
.team-card {
  background-color: #374785 !important;
  color: white;
  border: 1px solid transparent !important;
  border-radius: 2% !important;
}
</style>
