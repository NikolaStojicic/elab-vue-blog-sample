<template>
  <div class="home">
    <v-container>
      <v-row justify="end">
        <v-col cols="auto">
          <CardModal :item="modalItem" @addNewPost="newPost" />
        </v-col>
      </v-row>
      <v-row>
        <v-col v-for="(card, index) in arrayOfCards" :key="index">
          <BlogCard @editedItem="editItem" :item="card" />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import BlogCard from "@/components/BlogCard.vue";
import CardModal from "@/components/CardModal.vue";

export default {
  name: "Home",
  components: {
    BlogCard,
    CardModal
  },
  data() {
    return {
      arrayOfCards: [],
      modalItem: {
        title: "",
        subtitle: "",
        content: "",
        img: "no-img"
      }
    };
  },
  methods: {
    async newPost(payload) {
      this.modalItem = {
        title: "",
        subtitle: "",
        content: "",
        img: "no-img"
      };

      await this.$axios.post("http://localhost:5000/card", payload);
      await this.refreshContent();
    },
    async editItem(payload) {
      const id = payload.id;
      await this.$axios.put(`http://localhost:5000/card/${id}`, payload);
      this.refreshContent();
    },
    async refreshContent() {
      const res = await this.$axios.get("http://localhost:5000/cards");
      this.arrayOfCards = res.data;
    }
  },
  async created() {
    await this.refreshContent();
  }
};
</script>
