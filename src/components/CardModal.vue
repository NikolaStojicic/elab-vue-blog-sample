<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn :text="flat" color="primary" dark v-bind="attrs" v-on="on">
          <span v-if="myItem.id">Edit item</span>
          <span v-else>Add item</span>
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span v-if="myItem.id" class="headline">Edit post</span>
          <span v-else class="headline">New post</span>
        </v-card-title>
        <v-card-text>
          <v-form v-model="validForm">
            <v-container>
              <v-row>
                <v-col cols="12">
                  <v-text-field
                    v-model="myItem.title"
                    :rules="[v => !!v || 'Item is required']"
                    label="Title*"
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    v-model="myItem.subtitle"
                    :rules="[v => !!v || 'Item is required']"
                    label="Subtitle*"
                    outlined
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-textarea v-model="myItem.content" label="Content" outlined></v-textarea>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    v-model="myItem.img"
                    :rules="[v => !!v || 'Item is required']"
                    label="Image link*"
                    outlined
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="dialog = false">Close</v-btn>
          <v-btn color="primary" @click="saveBtn">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    validForm: false,
    myItem: null
  }),
  props: {
    item: {
      type: Object,
      required: true
    },
    flat: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    saveBtn() {
      if (this.validForm) {
        if (this.item.id) {
          this.$emit("editPost", this.myItem);
        } else {
          this.$emit("addNewPost", this.myItem);
          this.myItem = {
            title: "",
            subtitle: "",
            content: "",
            img: ""
          };
        }
        this.dialog = false;
      }
    }
  },
  created() {
    this.myItem = JSON.parse(JSON.stringify(this.item));
  }
};
</script>
