<template>
  <div>
    <ApolloQuery :query="require('../apollo/queries/currentProfile.gql')">
      <template slot-scope="{ result: { loading, error, data } }">
        <div v-if="loading" class="loading apollo">Loading...</div>
        <div v-else-if="error" class="error apollo">
          An error occured {{ error }}
        </div>

        <div v-else-if="data" class="result apollo">
          <div class="hero is-medium">
            <div class="hero-body background-image has-text-centered">
              <div class="container">
                <img
                  :src="
                    'https://ui-avatars.com/api/?name=' +
                      data.currentUser.identifier +
                      '&size=512&background=3FBE79&color=fefefe'
                  "
                  class="round"
                  width="250rem"
                />
                <h3
                  v-if="data.currentUser.city"
                  class="title has-text-white is-size-2 is-uppercase"
                >
                  {{ data.currentUser.city.name }}
                </h3>
                <h4
                  v-if="data.currentUser.name"
                  class="title is-size-5 has-text-white is-uppercase"
                >
                  {{ data.currentUser.name }}
                </h4>
              </div>
            </div>
          </div>
        </div>
        <div v-else class="no-result apollo">No result :(</div>
      </template>
    </ApolloQuery>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";

@Component({
  components: {}
})
export default class OmoProfile extends Vue {}
</script>

<style lang="scss" scoped>
.round {
  border: 5px solid #fff;
  border-radius: 100%;
  background-color: #fefefe;
}
.background-image {
  background-image: linear-gradient(
      to bottom,
      rgba(80, 80, 80, 0.3) 0%,
      rgba(82, 82, 82, 0.3) 100%
    ),
    url("/cities/munich2.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
