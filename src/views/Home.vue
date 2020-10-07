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
      arrayOfCards: [
        {
          id: 1,
          title: "Title1",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        },
        {
          id: 2,
          title: "Title2",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        },
        {
          id: 3,
          title: "Title3",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        },
        {
          id: 4,
          title: "Title4",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        },
        {
          id: 5,
          title: "Titl5",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        },
        {
          id: 6,
          title: "Title6",
          subtitle: "Subtitle1",
          content: "Content1",
          img: "no-img"
        }
      ],
      counter: 0,
      modalItem: {
        title: "",
        subtitle: "",
        content: "",
        img: "no-img"
      }
    };
  },
  methods: {
    newPost(payload) {
      this.modalItem = {
        title: "",
        subtitle: "",
        content: "",
        img: "no-img"
      };
      this.arrayOfCards.push({ ...payload, id: ++this.counter });
    },
    editItem(payload) {
      const id = payload.id;
      const cardById = this.arrayOfCards.find(el => el.id === id);
      cardById.title = payload.title;
      cardById.subtitle = payload.subtitle;
      cardById.content = payload.content;
      cardById.img = payload.img;
    }
  },
  created() {
    this.counter = this.arrayOfCards.length;
  }
};
</script>
