<template>
  <v-card class="mt-4 elevation-12">
    <v-toolbar dark color="primary">
      <v-toolbar-title>振込先口座を選択して下さい</v-toolbar-title>
    </v-toolbar>
    <v-card-text>
      <v-form>
        <v-select
          item-text="name"
          item-value="id"
          :items="accounts(branchId).filter(a => a.id !== id)"
          @input="$store.commit('transfer/accountId', $event)"
        />
        <v-btn nuxt dark to="branch" color="red" :disabled="!bankId">
          戻る
        </v-btn>
        <v-btn nuxt dark to="amount" color="primary" :disabled="!accountId">
          次へ
        </v-btn>
      </v-form>
      <!-- <code>{{ accounts(branchId) | json }}</code> -->
    </v-card-text>
  </v-card>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  middleware: ["hasBank", "hasBranch"],
  computed: {
    ...mapGetters("accounts", ["accounts"]),
    ...mapGetters("login", ["id"]),
    ...mapGetters("transfer", ["bankId", "branchId", "accountId"]),
  },
};
</script>
