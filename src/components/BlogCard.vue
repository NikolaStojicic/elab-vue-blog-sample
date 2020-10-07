<template>
  <v-card class="mx-auto" max-width="344">
    <v-img
      :src="item.img !== 'no-img'? item.img:'https://cdn.vuetifyjs.com/images/cards/sunshine.jpg' "
      height="200px"
    ></v-img>

    <v-card-title>{{item.title}}</v-card-title>

    <v-card-subtitle>{{item.subtitle}}</v-card-subtitle>

    <v-card-actions>
      <CardModal @editPost="editPost" class="ml-n16" :flat="true" :item="item" />
      <v-spacer></v-spacer>

      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>{{item.content}}</v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>

<script>
import CardModal from "@/components/CardModal.vue";
export default {
  components: {
    CardModal
  },
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    show: false
  }),
  methods: {
    editPost(payload) {
      this.$emit("editedItem", payload);
    }
  }
};
</script>

<style lang="scss" scoped>
</style>