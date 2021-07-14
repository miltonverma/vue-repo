<template>
  <div class="mb-6">
    <section class="hero is-medium is-primary is-bold mb-6">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Get GitHub Repositories</h1>
          <h2 class="subtitle">using Vue JS, REST API </h2>
        </div>
      </div>
    </section>
	<div class="container">
            <input placeholder="Search" v-model="reponame" name="searchVar"><b-button @click="getRepo()">Click here</b-button><p><b>Hint:</b> repos/miltonverma/exponent-cms</p>
	</div>
	<div class="container">
      <div class="table-container">
        <table class="table is-bordered is-striped is-hoverable is-fullwidth">
          <thead>
            <tr><th>ID</th><th>Author</th>
              <th>Date</th>
              <th>Commit</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="repodata in reposarr" :key="repodata">
              <td>{{ repodata.key }}</td>
              <td>{{ repodata.commit.author.name }}</td>
              <td>{{ repodata.commit.author.date }}</td>
              <td>{{ repodata.sha }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
	
	
    <div class="container">
      <div class="table-container">
        <table class="table is-bordered is-striped is-hoverable is-fullwidth">
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>URL</th>
              <th>Language</th>
              <th>Login</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="repo in repos" v-bind:key="repo.id">
              <td>{{ repo.id }}</td>
              <td>{{ repo.name }}</td>
              <td>{{ repo.html_url }}</td>
              <td>{{ repo.language }}</td>
              <td>{{ repo.owner.login }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Repository",
  data() {
    return {
      repos: null,reposarr: null,
      reponame: 'repos/miltonverma/exponent-cms',
    };
  },
  methods: {
    getRepo(){
       
axios.get("https://api.github.com/"+this.reponame+"/commits?per_page=25&page=1").then((response) => {
      this.reposarr = response.data;
    });	
	
    },
  },
  mounted(){
  this.getRepo();
  },
  created: function () {
    axios.get("https://api.github.com/users/miltonverma/repos").then((response) => {
      this.repos = response.data;
    });
  },
};
</script>

<style>
body {
  font: 15px/1.8 "Poppins", sans-serif !important;
}

.table td,
.table th {
  padding: 20px !important;
}

</style>