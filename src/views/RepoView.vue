<template>
  <main>
    <div class="back_btn">
      <RouterLink to="/repos">
        <button class="back">Go back</button>
      </RouterLink>
    </div>
    <div class="repo_container">
      <div class="repo_card">
        <div class="repo_items">
          <h4>Repo Name:</h4>
          <p> {{ repo.name }}</p>
        </div>
        <div class="repo_items">
          <h4>Description:</h4>
          <p>{{ repo.description ? repo.description : 'No Description yet' }}</p>
        </div>
        <div class="repo_items">
          <h4>Language:</h4>
          <p>{{ repo.language }}</p>
        </div>
      </div>
      <div class="repo_card">
        <div class="repo_items">
          <h4>Created:</h4>
          <p
            >{{ convertDate(repo.created_at) }}
            {{ getTime(repo.created_at) }}
          </p>
        </div>
        <div class="repo_items">
          <h4>Updated:</h4>
          <p>
            {{ convertDate(repo.updated_at) }}
            {{ getTime(repo.updated_at) }}
          </p>
        </div>
        <div class="repo_items">
          <h4>Push:</h4>
          <p>
            {{ convertDate(repo.pushed_at) }}
            {{ getTime(repo.pushed_at) }}
          </p>
        </div>
      </div>
      <div class="repo_card">
        <div class="repo_items">
          <h4>Repo size:</h4>
          <p>{{ repo.size }}kb</p>
        </div>
        <div class="repo_items">
          <h4>Stars:</h4>
          <p> {{ repo.stargazers_count }}</p>
        </div>
        <div class="repo_items">
          <h4>Watchers:</h4>
          <p> {{ repo.watchers_count }}</p>
        </div>
      </div>
      <div class="repo_card">
        <div class="repo_items">
          <h4>Forks</h4>
          <p>{{ repo.forks_count }}</p>
        </div>
        <div class="repo_items">
          <h4>Issues:</h4>
          <p>{{ repo.open_issues_count }}</p>
        </div>
        <div class="repo_items">
          <h4>Subscribers:</h4>
          <p>{{ repo.subscribers_count }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'RepoView',
  data() {
    return {
      repo: {}
    }
  },

  methods: {
    async fetchRepo() {
      const response = await fetch(
        `https://api.github.com/repos/Shile01/${this.$route.params.id}`
      )
      const data = await response.json()
      console.log(data)
      this.repo = data
    },

    convertDate(date) {
      const newDate = new Date(date)
      return newDate.toLocaleDateString()
    },
    // get time from date
    getTime(date) {
      const newDate = new Date(date)
      return newDate.toLocaleTimeString()
    }
  },

  mounted() {
    this.fetchRepo()
  }
}
</script>

<style scoped>
/* main {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding-bottom: 40px;
} */

main {
  /* min-height: 100vh; */
  display: flex;
  flex-direction: column;
  padding: 40px 24px;
  max-width: 1280px;
  width: 100%;
  margin: 0 auto;
}


.back_btn {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  width: 100%;
}

.back_btn a {
  text-decoration: none;
}

.back {
  font-size: 16px;
  border: 1px solid #002147;
  color: #fff;
  text-align: center;
  padding: 16px 32px;
  border-radius: 8px;
  background-color: #002147;
  transform: transform 250ms ease;
  margin-bottom: 24px;
}

.back:hover,.back:focus {
  background-color: #f1f1e6;
  color: #002147;
  border: 1px solid #002147;
  /* transform: scale(1.05); */
}

.repo_container {
  background-color: #fff;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px 20px;
  width: 100%;
  border-radius: 8px;
}

.repo_items {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 10px;
  justify-content: space-between;
  background-color: #e5f0ff;
}

.repo_items span:nth-child(1) {
  font-weight: bold;
  white-space: nowrap;
}

.repo_items span:nth-child(2) {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.repo_container >  *  {
  border-top: 1px solid #002147;
}

.repo_card h4 {
  font-weight: 400;
}

.repo_card p{
font-size: 14px;
}


@media (max-width: 768px) {
  .repo_container {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  }
}
</style>
