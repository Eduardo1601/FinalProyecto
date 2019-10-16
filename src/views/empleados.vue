/* eslint-disable */
<template>
  <div id="app">
    <md-toolbar class="md-primary" md-elevation="1">
      <h3 class="md-title" style="flex: 1">Empleados</h3>
      <md-button>Regresar</md-button>
      <md-button class="md-primary">Perfil</md-button>
    </md-toolbar>
    <md-table v-model="searched" md-sort="name" md-sort-order="asc" md-card md-fixed-header>
      <md-table-toolbar>
        <div class="md-toolbar-section-start">
          <h1 class="md-title">EMPLEADOS</h1>
        </div>
        <md-field md-clearable class="md-toolbar-section-end">
          <md-input placeholder="Buscar por nombre..." v-model="search" @input="searchOnTable" />
        </md-field>
      </md-table-toolbar>

      <md-table-empty-state
        md-label="No se encontro el empleado"
        :md-description="`No se encontraron coincidencias. Intenta con un nombre diferente o crea un usuario con ese nombre.`"
      >
        <md-button class="md-primary md-raised" @click="showDialog=true">Crear usuario</md-button>
      </md-table-empty-state>

      <md-table-row slot="md-table-row" slot-scope="{item}">
        <md-table-cell md-label="Nombres" md-sort-by="nombre">{{item.nombre}}</md-table-cell>
        <md-table-cell md-label="Apellidos" md-sort-by="apellido">{{ item.apellido }}</md-table-cell>
        <md-table-cell md-label="Fecha Ingreso" md-sort-by="fechaIngreso">{{ item.fechaIngreso }}</md-table-cell>
        <md-table-cell md-label="Email" md-sort-by="email">{{ item.email }}</md-table-cell>
        <md-table-cell md-label="DPI" md-sort-by="dpi">{{ item.dpi }}</md-table-cell>
        <md-table-cell>
          <md-button class="md-fab md-mini md-primary">
            <i class="material-icons">edit</i>
          </md-button>

          <md-button class="md-fab md-mini">
            <i class="material-icons">delete</i>
          </md-button>
        </md-table-cell>
      </md-table-row>
    </md-table>
    <md-speed-dial :class="bottomPosition">
      <md-speed-dial-target @click="showDialog=true">
        <md-icon>add</md-icon>
      </md-speed-dial-target>
    </md-speed-dial>

    <md-dialog :md-active.sync="showDialog">
      <div>
        <form novalidate class="md-layout" @submit.prevent="validateUser">
          <md-card class="md-layout-item">
            <md-card-header>
              <div class="md-title">Crear Empleado</div>
            </md-card-header>

            <md-card-content>
              <div class="md-layout md-gutter">
                <div class="md-layout-item">
                  <md-field :class="getValidationClass('firstName')">
                    <label for="first-name">Nombre(s)</label>
                    <md-input
                      name="first-name"
                      id="first-name"
                      autocomplete="given-name"
                      v-model="form.firstName"
                      :disabled="sending"
                    />
                    <span
                      class="md-error"
                      v-if="!$v.form.firstName.required"
                    >The first name is required</span>
                    <span
                      class="md-error"
                      v-else-if="!$v.form.firstName.minlength"
                    >Invalid first name</span>
                  </md-field>
                </div>

                <div class="md-layout-item md-small-size-100">
                  <md-field :class="getValidationClass('lastName')">
                    <label for="last-name">Apellido(s)</label>
                    <md-input
                      name="last-name"
                      id="last-name"
                      autocomplete="family-name"
                      v-model="form.lastName"
                      :disabled="sending"
                    />
                    <span
                      class="md-error"
                      v-if="!$v.form.lastName.required"
                    >The last name is required</span>
                    <span class="md-error" v-else-if="!$v.form.lastName.minlength">Invalid last name</span>
                  </md-field>
                </div>
              </div>
              
              <div>
                <md-field>
                  <label>DPI</label>
                                  <md-input
                  type="number"
                  name="number"
                  id="number"
                  autocomplete="number"
                  v-model="form.number"
                  :disabled="sending"
                />
                </md-field>
                <span
                      class="md-error"
                      v-if="!$v.form.number.required"
                    >The number is required</span>
              </div>

              <md-field :class="getValidationClass('email')">
                <label for="email">Email</label>
                <md-input
                  type="email"
                  name="email"
                  id="email"
                  autocomplete="email"
                  v-model="form.email"
                  :disabled="sending"
                />
                <span class="md-error" v-if="!$v.form.email.required">The email is required</span>
                <span class="md-error" v-else-if="!$v.form.email.email">Invalid email</span>
              </md-field>
            </md-card-content>

            <md-progress-bar md-mode="indeterminate" v-if="sending" />

            <md-card-actions>
              <md-button class="md-primary" @click="showDialog = false">Close</md-button>
              <md-button type="submit" class="md-primary" :disabled="sending">Create user</md-button>
            </md-card-actions>
          </md-card>

          <md-snackbar :md-active.sync="userSaved">The user {{ lastUser }} was saved with success!</md-snackbar>
        </form>
      </div>
    </md-dialog>
  </div>
</template>

<script>
/* eslint-disable */
import { validationMixin } from "vuelidate";
import axios from "axios";
import {
  required,
  date,
  email,
  minLength,
  maxLength
} from "vuelidate/lib/validators";
const toLower = text => {
  return text.toString().toLowerCase();
};

const searchByName = (items, term) => {
  if (term) {
    return items.filter(item => toLower(item.nombre).includes(toLower(term)));
  }

  return items;
};

export default {
  name: "TableSearch",
  mixins: [validationMixin],
  mounted() {
    this.getTodos();
  },
  data: () => ({
    form: {
      firstName: null,
      lastName: null,
      number: null,
      email: null,
    },
    userSaved: false,
    sending: false,
    lastUser: null,
    search: null,
    searched: [],
    users: [],
    showDialog: false,
    bottomPosition: "md-bottom-right",
    selectedDate: null,
    disabledDates: date => {
      const day = date.getDay();

      return day === 6 || day === 0;
    }
  }),
  validations: {
    form: {
      firstName: {
        required,
        minLength: minLength(3)
      },
      lastName: {
        required,
        minLength: minLength(3)
      },
      email: {
        required,
        email
      },
      number: {
        required
      },
    }
  },
  methods: {
    newUser() {},
    searchOnTable() {
      this.searched = searchByName(this.users, this.search);
    },
    getValidationClass(fieldName) {
      const field = this.$v.form[fieldName];

      if (field) {
        return {
          "md-invalid": field.$invalid && field.$dirty
        };
      }
    },
    clearForm() {
      this.$v.$reset();
      this.form.firstName = null;
      this.form.lastName = null;
      this.form.age = null;
      this.form.gender = null;
      this.form.email = null;
    },
    saveUser() {
      this.sending = true;
    },
    validateUser() {
      this.$v.$touch();

      if (!this.$v.$invalid) {
        this.saveUser();
      }
    },
    getTodos() {
      axios
        .get("http://localhost:3000/empleados", {})
        .then(response => {
          this.search =""  ;
          this.users = response.data;
          
        })
        
        .catch(e => console.log(e));
    }
  },
  created() {
    this.searched = this.users;
  }
};
</script>

<style lang="scss" scoped>
.md-table {
  width: 100%;
  height: 100%;
  border-collapse: collapse;
  padding: 5%;
}
.md-table-row {
  background-color: rgb(184, 180, 180);
  width: 30%;
  padding: 0%;
}
.md-table-cell {
  background-color: white;
  width: 0%;
}
.users {
  font-family: verdana;
}
.md-title {
  font-weight: bold;
}
.md-title {
  text-align: left;
}
.md-fab {
  color: rgb(102, 30, 30);
  align-self: right;
}
.material-icons {
  color: white;
}

.md-field {
  max-width: 300px;
}
.md-dialog {
  max-width: 768px;
}
.md-progress-bar {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
}
</style>