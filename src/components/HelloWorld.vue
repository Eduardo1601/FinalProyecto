
<template>
  <div class="page-container">
    <md-app>
      <md-app-toolbar class="md-primary" md-elevation="0">
        <md-button class="md-icon-button" @click="toggleMenu" v-if="!menuVisible">
           <div>
      <md-icon md-src="/assets/reorder-24px.svg" />
        </div>
        </md-button>
         <div>
      <md-icon md-src="/assets/reorder-24px.svg" />
        </div>
        <span class="md-title">My Title</span>
      </md-app-toolbar>

      <md-app-drawer :md-active.sync="menuVisible" md-persistent="mini">
        <md-toolbar class="md-transparent" md-elevation="0">
          <md-list-item>
          <md-avatar>
            <img src="https://placeimg.com/40/40/people/6" alt="People">
          </md-avatar>
          <span class="md-list-item-text">Mary Johnson</span>
        </md-list-item>

          <div class="md-toolbar-section-end">
            <md-button class="md-icon-button md-dense" @click="toggleMenu">
            </md-button>
          </div>
        </md-toolbar>

          <md-list-item>
            <md-button class="dos" @click="toggleMenu">Perfil</md-button> 
          </md-list-item>

          <md-list-item>
            <md-button class="uno" @click="toggleMenu">Solicitudes</md-button>
          </md-list-item>

        </md-list>
      </md-app-drawer>

      <md-app-content>
      </md-app-content>
    </md-app>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data: () => ({
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
