<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="danger">
      <router-link
        :to="{ name: 'main' }"
        tag="b-navbar-brand"
        style="cursor: pointer"
        >Home</router-link
      >
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <router-link :to="{ name: 'search' }" tag="b-nav-item"
            >Search</router-link
          >
          <router-link :to="{ name: 'about' }" tag="b-nav-item"
            >About</router-link
          >
        </b-navbar-nav>

        <b-navbar-nav class="ml-auto" v-if="!$root.store.username" right>
          <b-button variant="danger" disabled>hello guest</b-button>
          <router-link :to="{ name: 'login' }" tag="b-nav-item"
            >Login</router-link
          >
          <router-link :to="{ name: 'register' }" tag="b-nav-item"
            >Register</router-link
          >
        </b-navbar-nav>
        <b-navbar-nav class="ml-auto" v-else right>
          <b-button variant="danger" disabled>{{
            $root.store.username
          }}</b-button>
          <b-nav-item-dropdown>
            <template #button-content>
              <em>Personal</em>
            </template>
            <router-link :to="{ name: 'myFavorites' }" tag="b-dropdown-item"
              >My Favorites <i class="fas fa-star" style="color: gold;"></i></router-link
            >
            <router-link :to="{ name: 'myRecipes' }" tag="b-dropdown-item"
              >My Recipes</router-link
            >
            <router-link :to="{ name: 'myFamilyRecipes' }" tag="b-dropdown-item"
              >My Family Recipes</router-link
            >
          </b-nav-item-dropdown>
          <b-button
            variant="danger"
            class="add-recipe-button"
            @click="() => this.$emit('inputChange', true)"
          >
            Add New Recipe
          </b-button>
          <b-button
            @click="
              () => {
                logout();
                // this.$router.push('/');
              }
            "
            variant="outline-light"
            >Logout</b-button
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  methods: {
    async logout() {
      try {
        const response = await this.axios.post(
          this.$root.store.server_domain + "/Logout"
        );
        this.$emit('Logout');
      } catch (err) {
        console.log(err.response);
      }
    },
  },
};
</script>

<style>
</style>