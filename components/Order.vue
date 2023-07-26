<template>
  <v-row>
    <v-col cols="12">
      <h2>Order</h2>
      <v-list>
        <v-list-item v-for="(item, index) in cartItems" :key="index">
          <v-list-item-content>
            <v-list-item-title>
              {{ item.title }}
            </v-list-item-title>

            <v-list-item-subtitle>
              {{ currency(item.price) }} X
              <v-btn
                x-small
                icon
                color="primary"
                class="px-0"
                @click="decrement(item.id)"
              >
                <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
              {{ item.quantity }}
              <v-btn
                x-small
                icon
                color="primary"
                class="px-0"
                @click="increment(item.id)"
              >
                <v-icon>mdi-chevron-up</v-icon>
              </v-btn>
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn x-small icon color="error" @click="remove(item.id)">
              <v-icon>mdi-close-thick</v-icon>
            </v-btn>
            {{ currency(itemTotal(item.price, item.quantity)) }}
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>

<script>
import { mapState, mapGetters, mapActions } from "vuex";

export default {
  methods: {
    currency(value) {
      return Intl.NumberFormat("en-US").format(value);
    },

    ...mapActions("carts", {
      increment: "increment",
      decrement: "decrement",
      remove: "remove",
    }),
  },

  computed: {
    ...mapState("carts", {
      items: "items",
    }),

    ...mapGetters("carts", {
      cartItems: "cartItem",
      itemTotal: "itemTotal",
    }),
  },
};
</script>
