<template>
  <div class="login mt-5">
    <div class="card">
      <div class="card-header">
        Inscrivez-vous
      </div>
      <div class="card-body">
        <form>
          <div class="form-group">
            <label for="email">Nom légal de votre établissement</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': errors.nom }"
              id="name"
              v-model="details.nom"
              placeholder="Entrer le nom de votre établissement"
            />
            <div class="invalid-feedback" v-if="errors.nom">
              {{ errors.nom[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="email">Telephone</label>
            <input
              type="text"
              class="form-control"
              :class="{ 'is-invalid': errors.telephone }"
              id="name"
              v-model="details.numero"
              placeholder="entrer votre no de telephone"
            />
            <div class="invalid-feedback" v-if="errors.telephone">
              {{ errors.name[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              class="form-control"
              :class="{ 'is-invalid': errors.email }"
              id="email"
              v-model="details.email"
              placeholder="Entrer votre email"
            />
            <div class="invalid-feedback" v-if="errors.email">
              {{ errors.email[0] }}
            </div>
          </div>
           <div class="form-group">
            <label for="email">Adresse de l'établissement</label>
            <input
              type="email"
              class="form-control"
              :class="{ 'is-invalid': errors.adresse }"
              id="email"
              v-model="details.adresse"
              placeholder="Entrer votre adresse"
            />
            <div class="invalid-feedback" v-if="errors.adresse">
              {{ errors.adresse[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="password">Mot de passe</label>
            <input
              type="password"
              class="form-control"
              :class="{ 'is-invalid': errors.motDePasse }"
              id="password"
              v-model="details.mot_de_passe"
              placeholder="Password"
            />
            <div class="invalid-feedback" v-if="errors.password">
              {{ errors.password[0] }}
            </div>
          </div>
          <div class="form-group">
            <label for="password_confirmation">Confirmation du mot de passe</label>
            <input
              type="password"
              class="form-control"
              id="password_confirmation"
              v-model="details.mot_de_passe_confirmation"
              placeholder="Confirm password"
            />
          </div>
          <button type="button" @click="register" class="btn btn-primary">
            Inscription
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Home",

  data: function() {
    return {
      details: {
        email: null,
        numero: null,
        mot_de_passe: null,
        mot_de_passe_confirmation: null,
        type_createur : "E",
        nom : null,
        adresse: null
      }
    };
  },

  computed: {
    ...mapGetters(["errors"])
  },

  mounted() {
    this.$store.commit("setErrors", {});
  },

  methods: {
    ...mapActions("auth", ["sendRegisterEstablishmentRequest"]),

    register: function() {
      this.sendRegisterEstablishmentRequest(this.details).then(() => {
        this.$router.push({ name: "Home" });
      });
    }
  }
};
</script>
