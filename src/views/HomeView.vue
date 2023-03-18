<template>
  <main>
    <div class="user-container">
      <!-- user section -->
      <div class="user_section">
        <div class="user_profile_section">
          <div class="img-card">
            <img :src="user.avatar_url" alt="profile_img" />
          </div>
          <div class="user_profile_name">
            <h2>{{ user.name }}</h2>
            <p class="username">{{ user.login }}</p>
          </div>
        </div>
        <div class="group-btn">
          <div class="repo_btn">
              <RouterLink to="/repos">
                <p>View Repositories</p>
              </RouterLink>
            </div>
          <div class="profile_btn">
            <a :href="user.html_url" target="_blank">
              <button>View Profile</button>
            </a>
          </div>

        </div>
      </div>
    </div>
    <!-- end of user section -->
    <!-- section for user information -->
    <section class="information_section">
      <div class="user_container_grid">
        <div class="user_container_bio">
            <!-- section for user information -->
            <h3>Bio 🧔</h3>
            <div class="user_bio">
              <p class="user-bio">{{ user.bio }}</p>
            </div>
          </div>

        <div class="user_container_bio">
          <!-- section for user information -->
          <h3>My Info  💼  </h3>
          <div class="user_bio">
            <div class="email">
              <p>{{ user.email ? user.email : 'intouchwithola@gmail.com' }}</p>
            </div>
            <div class="location">
              <p>{{ user.location }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="social_card_container">
        <h3>Page Stats 📈</h3>
        <div class="social_card">
          <p>Followers</p>
          <span>{{ user.followers }}</span>
        </div>
        <div class="social_card">
            <p>Following</p>
            <span>{{ user.following }}</span>
          </div>
        <div class="social_card">
          <p>Public Repositories</p>
          <span>{{ user.public_repos }}</span>
        </div>
        <div class="social_card">
          <p>Gists</p>
          <span>{{ user.public_gists }}</span>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      user: {}
    }
  },

  methods: {
    async getUser() {
      const response = await fetch('https://api.github.com/users/Shile01')
      const data = await response.json()
      this.user = data
    }
  },
  created() {
    this.getUser()
  }
}
</script>

<style scoped>
main {
  /* min-height: 100vh; */
  display: flex;
  flex-direction: column;
  padding: 40px 24px;
  max-width: 1280px;
  width: 100%;
  margin: 0 auto;
}

.user_section {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 28px;
}

.user_profile_section {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 16px !important;
}
.img-card {
  width: 320px;
  height: 320px;
  border-radius: 8px;
  overflow: hidden;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.user_profile_name {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.user_profile_name h2 {
  font-size: 28px;
  font-weight: 700;
}
.user_profile_name p {
  font-size: 20px;
  line-height: 20px;
  font-weight: 500;
  font-style: italic;
  /* border: 1px solid yellow; */
}

.group-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 24px;
}

.profile_btn button {
  background-color: #005d35;
  color: #fff;
  padding: 12px 24px;
  border: 1px solid #005d35;
  border-radius: 4px;
  /* font-size: 16px; */
  cursor: pointer;
}

.profile_btn button:hover {
  background: none;
  color: #005d35;
}
.repo_btn {
  padding-bottom: 2px;
  color: #002147;
  cursor: pointer;
  position: relative;
}

.repo_btn::after {
   content: "";
  position: absolute;
  width: 100%;
  height: 1px;
  background-color: currentColor;
  width: 100%;
  bottom: -2px;
  left: 0;
  right: 0;
  transform: scaleX(0);
  border-radius: 0.5rem;
  transform-origin: right;
  transition: transform 250ms ease;
}

.repo_btn:hover::after,
.repo_btn:focus::after {
  transform: scaleX(1);
  transform-origin: left;
  outline: none;
}


.information_section {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: flex-start;
  gap: 20px;
  margin-top: 52px;
}

.user_container_grid {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.user_container_bio {
  background-color: #f5f9ff;
  padding: 20px 40px;
  border-radius: 4px;
}

.user_container_bio h3 {
  font-size: 24px;
  line-height: 24px;
  font-weight: 600;
  color: #000;
}

.user_bio {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 5px;
  margin-top: 20px;
}

.user_bio .email p,
.user_bio .location p {
  font-size: 16px;
  line-height: 24px;
  font-weight: 500;
}

.social_card_container {
  background-color: #002147;
  color: #fff;
  padding: 20px 20px;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  border-radius: 4px;
}

.social_card_container h3 {
  font-size: 24px;
  line-height: 24px;
  font-weight: 600;
  color: #fff;
  margin-bottom: 10px;
}

.social_card {
  gap: 50px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  border-bottom: 1px solid #d9d9d9;
}


.user-details {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 10px;
}

.user-bio {
  white-space: wrap;
}

@media (max-width: 800px) {
  .user_section {
    left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .user_profile_section {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 5px;
  }

  .user_profile_name {
    text-align: center;
  }

  .information_section {
    width: 100%;
    flex-direction: column;
    margin-top: 40px;
    align-items: center;
  }
  .user_container_grid {
    width: 100%;
  }
  .social_card_container {
    width: 100%;
  }
}

/* @media (max-width: 376px) {
  .group-btn {
    flex-direction: column;
    gap: 10px;
  }
} */
</style>
