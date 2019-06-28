<template>
  <b-container class="content-container">
    <b-row class="mb-3">
      <b-col cols="6" class="ml-auto mr-auto">
        <b-form-input v-model="input" placeholder="Search for team..."></b-form-input>
      </b-col>
    </b-row>
    <b-row>
      <b-col class="team-container" cols="4" v-for="(team, index) in filteredTeam" :key="index">
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
import getStats from '../services/getStats.js'
export default {
  name: "Stats",
  data() {
    return {
      teams: [],
      input: '',
      error: false
    };
  },
  created() {
    getStats.getDynamicScores().then(response => {
      this.teams = response.data.teams
    })
  },
  computed: {
    filteredTeam() {
      return this.teams.filter(team => {
        let teamName = `${team.team.city} ${team.team.name}`
        return teamName.toLowerCase().includes(this.input.toLowerCase())

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
