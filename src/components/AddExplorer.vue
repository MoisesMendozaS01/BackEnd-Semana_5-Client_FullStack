<template>
  <div class="submit-form">
    <div v-if="!submitted">
    <h3>Nuevo Explorer</h3>
      <div class="form-group">
        <label for="title">Nombre </label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          v-model="explorer.name"
          name="title"
        />
      </div>
      <div class="form-group">
        <label for="title">Username</label>
        <input
          type="text"
          class="form-control"
          id="username"
          required
          v-model="explorer.username"
          name="username"
        />
      </div>
      <div class="form-group">
        <label for="title">Main Stack</label>
        <input
          type="text"
          class="form-control"
          id="mainStack"
          required
          v-model="explorer.mainStack"
          name="mainStack"
        />
      </div>
      <button @click="saveExplorer" class="btn btn-success">Agregar</button>
    </div>
    <div v-else>
      <h4> Explorer creado exitosamente. </h4>
      <button class="btn btn-success" @click="newExplorer">Add</button>
    </div>
  </div>
</template>

<script>
import ExplorerService from "../services/ExplorerService";
export default {
  name: "add-explorer",
  data() {
    return {
      explorer: {
        id: null,
        name: "",
        username: "",
        mainStack: ""
      },
      submitted: false
    };
  },
  methods: {
    saveExplorer() {
      var data = {
        name: this.explorer.name,
        username: this.explorer.username,
        mainStack: this.explorer.mainStack
      };
      ExplorerService.create(data)
        .then(response => {
          this.explorer.id = response.data.id;
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    newExplorer() {
      this.submitted = false;
      this.explorer = {};
    }
  }
};
</script>
