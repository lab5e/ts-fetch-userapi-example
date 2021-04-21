<template>
  <div>
    <form>
      <fieldset>
        <legend>API Token</legend>
        <div>
          <input class="stretch" id="api-token" type="text" v-model="token" />
        </div>
      </fieldset>
    </form>
    <div class="button">
      <button id="load-profile" v-on:click="retrieveProfile()">
        Load profile
      </button>
    </div>
    <fieldset>
      <legend>Result</legend>
      <div>
        <label for="name">Name</label>
        <input
          id="name"
          class="field"
          readonly
          type="text"
          placeholder="Name goes here"
          v-model="profile.name"
        />
      </div>
      <div>
        <label for="email">Email</label>
        <input
          id="email"
          class="field"
          readonly
          type="text"
          placeholder="Email goes here"
          v-model="profile.email"
        />
      </div>
      <div>
        <label for="avatar-url">Avatar URL</label>
        <input
          id="avatar-url"
          class="field"
          readonly
          type="text"
          placeholder="Avatar URL goes here"
          v-model="profile.avatarUrl"
        />
      </div>
    </fieldset>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import {
  ProfileApi,
  Configuration,
  ConfigurationParameters,
  UserProfile,
} from "@lab5e/ts-fetch-userapi";

@Component
export default class ProfileDemo extends Vue {
  data(): {
    profile: UserProfile;
    token: string;
  } {
    return {
      profile: {},
      token: "",
    };
  }
  retrieveProfile(): void {
    // Create a ConfigurationParameters struct for the setup and assign the
    // apiKey property to the token.
    var params: ConfigurationParameters = {
      apiKey: this.$data.token,
    };
    // Create a Configuration instance with the parameters
    var config = new Configuration(params);

    // ...and create the ProfileApi instance.
    var profileApi = new ProfileApi(config);

    // Finally: userGetUserProfile returns the user profile
    profileApi
      .getUserProfile()
      .then((profile) => {
        this.$data.profile = profile;
      })
      .catch((err) => {
        err.text().then((message: string) => {
          alert("Error message: " + message);
        });
      });
  }
}
</script>

<style scoped>
button {
  font-size: 1em;
}
input {
  font-size: 1em;
  margin: 0.25em;
}
input.stretch {
  width: 750px;
}
input.field {
  width: 550px;
}
div {
  text-align: left;
}
div.button {
  padding-top: 1em;
  text-align: center;
}
fieldset {
  width: 800px;
  margin-left: auto;
  margin-right: auto;
}
label {
  margin: 0.5em;
  width: 100px;
  display: inline-block;
  font-weight: bold;
}
</style>