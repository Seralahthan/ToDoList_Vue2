<template>
  <div class="ui basic content center aligned segment">

    <button class="ui basic button icon" v-on:click="openForm" v-show="!isCreating">
      <i class="plus icon"></i>
    </button>

    <div class="ui centered card" v-show="isCreating">
      <div class="content">
        <div class="ui form">
          <div class="field">
            <label>Title</label>
            <input v-model="titleText" type="text" ref="title">
          </div>

          <div class="field">
            <label>Project</label>
            <input v-model="projectText" type="text" ref="project">
          </div>

          <div class="ui two button attached buttons">

            <button class="ui basic blue button" v-on:click="sendForm()">
              Create
            </button>

            <button class="ui basic red button" v-on:click="closeForm()">
              Cancel
            </button>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      "reaction"
    ],
    data() {
      return {
        titleText: "",
        projectText: "",
        isCreating: false,
      };
    },

    methods: {
      openForm() {
        this.isCreating = true;
      },
      closeForm() {
        this.isCreating = false;
      },
      sendForm() {
        if(this.titleText.length > 0 && this.projectText.length > 0) {
          this.reaction.title = this.titleText;
          this.reaction.project = this.projectText;
          this.reaction.done = false;
          this.$emit("create-todo", this.reaction);
        }
        this.isCreating = false;
        this.titleText = "";
        this.projectText = "";
      },
    },
  };
</script>
