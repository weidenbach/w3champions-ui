<template>
  <v-card-text>
    <v-row class="justify-center">
      <v-col class="text-center">
        <h3>
          You were invited by
          <b>{{ clanName }}</b>
          to join their ranks!
        </h3>
      </v-col>
    </v-row>

    <v-row class="justify-center">
      <v-col cols="3" class="text-center">
        <v-btn @click="joinClan">Join {{ clanName }} !</v-btn>
      </v-col>
      <v-col cols="3" class="text-center">
        <v-btn outlined @click="rejectClan">Reject invite</v-btn>
      </v-col>
    </v-row>
  </v-card-text>
</template>
<script lang="ts">
import Vue from "vue";
import { Component } from "vue-property-decorator";

@Component({})
export default class AcceptInvitePanel extends Vue {
  get clanName(): string {
    return this.$store.direct.state.clan.selectedMemberShip.clanName;
  }

  public async joinClan(): Promise<void> {
    await this.$store.direct.dispatch.clan.acceptInvite();
    await this.$store.direct.dispatch.clan.retrievePlayersClan();
    await this.$store.direct.dispatch.clan.retrievePlayersMembership();
  }

  public async rejectClan(): Promise<void> {
    await this.$store.direct.dispatch.clan.rejectInvite();
    await this.$store.direct.dispatch.clan.retrievePlayersClan();
    await this.$store.direct.dispatch.clan.retrievePlayersMembership();
  }
}
</script>
