<template>
  <main>
    <!-- ui card for git repo card list grid view -->
    <div class="repo_container_grid">
      <ul v-for="repo in paginateRepo" :key="repo.id">
        <li>{{ repo.name }}</li>
        <div class="repo_btn">
          <RouterLink :to="{ name: 'repo', params: { id: repo.name } }">
            <button>View</button>
          </RouterLink>
        </div>
      </ul>
    </div>
    <div class="pagination_container">
      <button
        @click="currentPage--"
        :disabled="currentPage === 1"
        :class="{ disabled: currentPage === 1 }"
      >
        Prev
      </button>
      <span>Page {{ currentPage }} of {{ totalPage }}</span>
      <button
        @click="currentPage++"
        :disabled="currentPage === totalPage"
        :class="{ disabled: currentPage === totalPage }"
      >
        Next
      </button>
    </div>
  </main>
</template>

<script>
export default {
  name: 'ReposView',
  data() {
    return {
      repos: [],
      currentPage: 1,
      perPage: 12,
      totalPage: 0
    }
  },

  methods: {
    async fetchRepo() {
      const response = await fetch('https://api.github.com/users/Shile01/repos')
      const data = await response.json()
      this.totalPage = Math.ceil(data.length / this.perPage)
      this.repos = data
    }
  },

  computed: {
    paginateRepo() {
      const startIndex = (this.currentPage - 1) * this.perPage
      const endIndex = startIndex + this.perPage
      return this.repos.slice(startIndex, endIndex)
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

.header_shadow {
  height: 165px;
  width: 100%;
  background-color: #d9d9d9;
  display: flex;
  align-items: center;
  justify-content: center;
}

.header_shadow i {
  font-size: 100px;
}
.repo_container_grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-gap: 24px;
  width: 100%;
  /* max-width: 900px; */
  padding: 10px 0;
  width: 100%;
}

ul {
  list-style: none;
  background-color: #fafaf0;
  border-radius: 8px;
  padding: 10px 20px;
  display: flex;
  gap: 20px;
  flex-direction: column;
  /* align-items: flex-end; */
  /* justify-content: flex-end; */
  width: 100%;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.1);
}

li {
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  text-transform: capitalize;
}

.repo_btn {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 100%;
}

.repo_btn > * > *{
  border: 1px solid #002147;
  color: #002147;
  background: none !important;
}

button {
  background-color: #fff;
  color: #000;
  padding: 12px 24px;
  border: 1px solid #e8e8e8;
  border-radius: 4px;
  cursor: pointer;
  overflow: hidden;
  transition: background 250ms ease-in-out;
}

button:hover {
  background-color:  hsla(0, 0%, 97%, 0.6);
  border: 1px solid black;

}

.pagination_container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin-top: 40px;
}

.disabled {
  cursor: not-allowed;
  opacity: 0.5;
  border: none !important;
}
</style>
