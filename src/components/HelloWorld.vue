
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
      <div>
        <md-table v-model="searched" md-sort="name" md-sort-order="asc" md-card md-fixed-header>
      <md-table-toolbar>
        <div class="md-toolbar-section-start">
          <h1 class="md-title">Users</h1>
        </div>

        <md-field md-clearable class="md-toolbar-section-end">
          <md-input placeholder="Search by name..." v-model="search" @input="searchOnTable" />
        </md-field>
      </md-table-toolbar>

      <md-table-empty-state
        md-label="No users found"
        :md-description="`No user found for this '${search}' query. Try a different search term or create a new user.`">
        <md-button class="md-primary md-raised" @click="newUser">Create New User</md-button>
      </md-table-empty-state>

      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="ID" md-sort-by="id" md-numeric>{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Name" md-sort-by="name">{{ item.name }}</md-table-cell>
        <md-table-cell md-label="Email" md-sort-by="email">{{ item.email }}</md-table-cell>
        <md-table-cell md-label="Gender" md-sort-by="gender">{{ item.gender }}</md-table-cell>
        <md-table-cell md-label="Job Title" md-sort-by="title">{{ item.title }}</md-table-cell>
      </md-table-row>
    </md-table>
        </div>
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
      search: null,
      searched: [],
      menuVisible: false,

      users: [
        {
          id: 1,
          name: "Shawna Dubbin",
          email: "sdubbin0@geocities.com",
          gender: "Male",
          title: "Assistant Media Planner"
        },
        {
          id: 2,
          name: "Odette Demageard",
          email: "odemageard1@spotify.com",
          gender: "Female",
          title: "Account Coordinator"
        },
        {
          id: 3,
          name: "Vera Taleworth",
          email: "vtaleworth2@google.ca",
          gender: "Male",
          title: "Community Outreach Specialist"
        },
        {
          id: 4,
          name: "Lonnie Izkovitz",
          email: "lizkovitz3@youtu.be",
          gender: "Female",
          title: "Operator"
        },
        {
          id: 5,
          name: "Thatcher Stave",
          email: "tstave4@reference.com",
          gender: "Male",
          title: "Software Test Engineer III"
        },
        {
          id: 6,
          name: "Karim Chipping",
          email: "kchipping5@scribd.com",
          gender: "Female",
          title: "Safety Technician II"
        },
        {
          id: 7,
          name: "Helge Holyard",
          email: "hholyard6@howstuffworks.com",
          gender: "Female",
          title: "Internal Auditor"
        },
        {
          id: 8,
          name: "Rod Titterton",
          email: "rtitterton7@nydailynews.com",
          gender: "Male",
          title: "Technical Writer"
        },
        {
          id: 9,
          name: "Gawen Applewhite",
          email: "gapplewhite8@reverbnation.com",
          gender: "Female",
          title: "GIS Technical Architect"
        },
        {
          id: 10,
          name: "Nero Mulgrew",
          email: "nmulgrew9@plala.or.jp",
          gender: "Female",
          title: "Staff Scientist"
        },
        {
          id: 11,
          name: "Cybill Rimington",
          email: "crimingtona@usnews.com",
          gender: "Female",
          title: "Assistant Professor"
        },
        {
          id: 12,
          name: "Maureene Eggleson",
          email: "megglesonb@elpais.com",
          gender: "Male",
          title: "Recruiting Manager"
        },
        {
          id: 13,
          name: "Cortney Caulket",
          email: "ccaulketc@cbsnews.com",
          gender: "Male",
          title: "Safety Technician IV"
        },
        {
          id: 14,
          name: "Selig Swynfen",
          email: "sswynfend@cpanel.net",
          gender: "Female",
          title: "Environmental Specialist"
        },
        {
          id: 15,
          name: "Ingar Raggles",
          email: "iragglese@cbc.ca",
          gender: "Female",
          title: "VP Sales"
        },
        {
          id: 16,
          name: "Karmen Mines",
          email: "kminesf@topsy.com",
          gender: "Male",
          title: "Administrative Officer"
        },
        {
          id: 17,
          name: "Salome Judron",
          email: "sjudrong@jigsy.com",
          gender: "Male",
          title: "Staff Scientist"
        },
        {
          id: 18,
          name: "Clarinda Marieton",
          email: "cmarietonh@theatlantic.com",
          gender: "Male",
          title: "Paralegal"
        },
        {
          id: 19,
          name: "Paxon Lotterington",
          email: "plotteringtoni@netvibes.com",
          gender: "Female",
          title: "Marketing Assistant"
        },
        {
          id: 20,
          name: "Maura Thoms",
          email: "mthomsj@webeden.co.uk",
          gender: "Male",
          title: "Actuary"
        }
      ]
    }),
    methods: {
      newUser () {
        window.alert('Noop')
      },
      searchOnTable () {
        this.searched = searchByName(this.users, this.search)
      },
      toggleMenu () {
        // eslint-disable-next-line 
        this.menuVisible = !this.menuVisible
        // eslint-disable-next-line 
      },
      // eslint-disable-next-line 
      menuVisible: false
    },
    created () {
      this.searched = this.users
    }
    }// eslint-disable-next-line 
    
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
 .md-field {
    max-width: 300px;
  }
  .md-toolbar + .md-toolbar {
    margin-top: 16px;
    background-color: blue;
    background-image: image("/assets/examples/logo.png")
  }
</style>
