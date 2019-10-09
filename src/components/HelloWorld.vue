
<template>
  <div class="page-container">
    <md-app>
      <md-app-toolbar class="md-primary" md-elevation="0">
        <md-button class="md-icon-button" @click="toggleMenu" v-if="!menuVisible">
           <div>
      <md-button class="md-icon-button md-raised md-accent">
        <md-icon></md-icon>
      </md-button>
        </div>
        </md-button>
         <div>
      <md-icon md-src="/assets/reorder-24px.svg" />
        </div>
        <span class="md-title">EsourceCapital</span>
      </md-app-toolbar>

      <md-app-drawer :md-active.sync="menuVisible" md-persistent="full">
        <md-toolbar class="md-transparent" md-elevation="0">
          <md-list-item>
          <md-avatar>
            <img src="https://placeimg.com/40/40/people/6" alt="People">
          </md-avatar>
          <span class="md-list-item-text">Carlos Salinas</span>
        </md-list-item>

          <div>
<md-button @click="toggleMenu" class="md-icon-button md-raised md-accent">
         <md-icon></md-icon>
        </md-button>
          </div>
        </md-toolbar>

          <md-dialog :md-active.sync="Perfil">
      <md-dialog-title>Preferences</md-dialog-title>

      <md-tabs md-dynamic-height>
        <md-tab md-label="General">
         <div>
    <md-card class="md-primary">
      <md-card-header>
        <md-card-header-text>
          <div class="md-title">Carlos Salinas</div>
          <div class="md-subhead">Desarrollo</div>
        </md-card-header-text>
        <md-card-media>
          <img src="https://placeimg.com/40/40/people/6" alt="Avatar">
        </md-card-media>
        </md-card-header>
        <md-card-actions>
        <md-button>Editar</md-button>
      </md-card-actions>
        </md-card>
  </div>
        </md-tab>

        <md-tab md-label="Activity">
         
        </md-tab>

        <md-tab md-label="Account">
         
        </md-tab>
      </md-tabs>

      <md-dialog-actions>
        <md-button class="md-primary" @click="Perfil = false">Close</md-button>
        <md-button class="md-primary" @click="Perfil = false">Save</md-button>
      </md-dialog-actions>
    </md-dialog>
  <md-list-item>
    <md-button class="md-primary md-raised" @click="Perfil = true">Perfil</md-button>
  </md-list-item>
      <md-list-item>
             <md-button class="md-raised md-primary">Solicitudes</md-button>
  </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <md-field>
      <label>Descripcióon</label>
      <md-input v-model="withLabel" placeholder="A nice placeholder"></md-input>
    </md-field>
    <md-button class="md-icon-button md-list-action">
            <md-icon class="md-primary"></md-icon>
          </md-button>
           <md-button class="md-raised md-accent">Denegado</md-button>
      <md-button class="md-raised md-primary">Aceptado</md-button>
      </md-app-content>
    </md-app>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data: () => ({
      Perfil: false,
      withLabel: null,
      // eslint-disable-next-line 
      menuVisible: false
    }),// eslint-disable-next-line 
    methods: {
      // eslint-disable-next-line 
      toggleMenu () {
        // eslint-disable-next-line 
        this.menuVisible = !this.menuVisible
        // eslint-disable-next-line 
      }
      // eslint-disable-next-line 
    }
    // eslint-disable-next-line 
  }
</script>

<style lang="scss" scoped>
  .md-dialog {
    max-width: 768px;
  }
  .md-app {
    min-height: 350px;
    border: 1px solid rgba(#000, .12);
  }

   // Demo purposes only
  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .md-toolbar + .md-toolbar {
    margin-top: 16px;
    background-color: blue;
    background-image: image("/assets/examples/logo.png")
  }
</style>
