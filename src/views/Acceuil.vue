<template>
  <div>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
      href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap"
      rel="stylesheet"
    />
    <!-- ------------------------------------------HEADER-------------------------------------------- -->
    <v-navigation-drawer v-model="drawer" absolute left temporary>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-title>Alertes</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>Mes evenements</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>Mes amis</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>Paramètres</v-list-item-title>
          </v-list-item>
          <v-list-item>
            <v-list-item-title @click.prevent="signOut"
              >Deconnexion</v-list-item-title
            >
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <degouline v-if="true" id="degouline"></degouline>

    <div>
      <div v-if="!user.loggedIn" class="divheader nonconnecte">
        <v-btn
          color="accent"
          elevation="4"
          raised
          rounded
          small
          text
          to="/Connexion"
          class="connexioninscription"
          >CONNEXION</v-btn
        >
        <v-btn
          color="accent"
          elevation="4"
          raised
          rounded
          small
          text
          class="connexioninscription"
          to="/Inscription"
          >INSCRIPTION</v-btn
        >
        <v-btn
          v-if="!user.loggedIn"
          color="accent"
          id="btncreerevent"
          elevation="4"
          raised
          rounded
          to="/Inscription"
          small
          text
        >
          CREER UN EVENEMENT
          <v-btn
            id="btncreereventredinterieur"
            color="accent"
            elevation="2"
            rounded
            small
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="7.582"
              height="12.519"
              viewBox="0 0 7.582 12.519"
            >
              <path
                id="Tracé_11"
                data-name="Tracé 11"
                d="M26.582,16.758v0a.82.82,0,0,0-.252-.592h0l-4.937-4.937,0,0a.822.822,0,1,0-1.105,1.218L24.6,16.758,20.23,21.125h0a.823.823,0,0,0,1.163,1.163h0l4.937-4.937h0a.82.82,0,0,0,.252-.592Z"
                transform="translate(-19.5 -10.5)"
                fill="#fff"
                stroke="#fff"
                stroke-width="1"
              />
            </svg>
          </v-btn>
        </v-btn>
        <v-btn
          v-if="user.loggedIn"
          color="accent"
          id="btncreerevent"
          elevation="4"
          raised
          rounded
          small
          text
        >
          CREER UN EVENEMENT
          <v-btn
            id="btncreereventredinterieur"
            color="accent"
            elevation="2"
            rounded
            small
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="7.582"
              height="12.519"
              viewBox="0 0 7.582 12.519"
            >
              <path
                id="Tracé_11"
                data-name="Tracé 11"
                d="M26.582,16.758v0a.82.82,0,0,0-.252-.592h0l-4.937-4.937,0,0a.822.822,0,1,0-1.105,1.218L24.6,16.758,20.23,21.125h0a.823.823,0,0,0,1.163,1.163h0l4.937-4.937h0a.82.82,0,0,0,.252-.592Z"
                transform="translate(-19.5 -10.5)"
                fill="#fff"
                stroke="#fff"
                stroke-width="1"
              />
            </svg>
          </v-btn>
        </v-btn>
      </div>
      <div v-if="user.loggedIn" class="divheaderconnecte">
        <div>
          <v-app-bar-nav-icon
            @click.stop="drawer = !drawer"
            class="btndrawer item"
          ></v-app-bar-nav-icon>
        </div>
        <div class="userconnected">
          <v-card class="titrecarduserheader">
            <v-card-title>{{ user.data.surname }}</v-card-title>
          </v-card>
        </div>

        <div>
          <v-btn
            to="/creationevent"
            color="accent"
            id="btncreerevent"
            elevation="4"
            raised
            rounded
            small
            text
          >
            CREER UN EVENEMENT
            <v-btn
              id="btncreereventredinterieur"
              color="accent"
              elevation="2"
              rounded
              small
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="7.582"
                height="12.519"
                viewBox="0 0 7.582 12.519"
              >
                <path
                  id="Tracé_11"
                  data-name="Tracé 11"
                  d="M26.582,16.758v0a.82.82,0,0,0-.252-.592h0l-4.937-4.937,0,0a.822.822,0,1,0-1.105,1.218L24.6,16.758,20.23,21.125h0a.823.823,0,0,0,1.163,1.163h0l4.937-4.937h0a.82.82,0,0,0,.252-.592Z"
                  transform="translate(-19.5 -10.5)"
                  fill="#fff"
                  stroke="#fff"
                  stroke-width="1"
                />
              </svg>
            </v-btn>
          </v-btn>
        </div>
      </div>
    </div>
    <img
      class="planetquitourne"
      style="position: absolute"
      src="@/assets/planetquitournerouge.gif"
    />
    <v-card class="titrecard">
      <v-card-title>T o o G e t h e r</v-card-title>
      <v-card-text
        >Faites des rencontres en faisant ce que vous aimez</v-card-text
      >
    </v-card>
    <div class="barrederecherchecontainer">
      <div class="barrederecherche">
        <div>
          <img class="pastille" src="@/assets/pastille.svg" alt="pastille" />
          <input
            id="inputrechercheevent"
            class="nomevent"
            type="text"
            :placeholder="placehorlderRecherche.nom"
          />
        </div>
        <div>
          <img class="pastille" src="@/assets/pastille.svg" alt="pastille" />
          <input
            class="endroit"
            id="inputrechercheevent"
            type="text"
            :placeholder="placehorlderRecherche.lieux"
          />
        </div>
        <div>
          <img class="pastille" src="@/assets/pastille.svg" alt="pastille" />
          <input
            class="date"
            id="inputrechercheevent"
            type="text"
            :placeholder="placehorlderRecherche.date"
          />
        </div>
        <v-btn
          to="/recherchevent"
          id="btncreereventredinterieur"
          color="accent"
          elevation="2"
          rounded
          small
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="7.582"
            height="12.519"
            viewBox="0 0 7.582 12.519"
          >
            <path
              id="Tracé_11"
              data-name="Tracé 11"
              d="M26.582,16.758v0a.82.82,0,0,0-.252-.592h0l-4.937-4.937,0,0a.822.822,0,1,0-1.105,1.218L24.6,16.758,20.23,21.125h0a.823.823,0,0,0,1.163,1.163h0l4.937-4.937h0a.82.82,0,0,0,.252-.592Z"
              transform="translate(-19.5 -10.5)"
              fill="#fff"
              stroke="#fff"
              stroke-width="1"
            />
          </svg>
        </v-btn>
      </div>
    </div>
    <div class="containerEtapes">
      <div class="premièreligne">
        <div class="deuxieme blocchiffretexteetapes">
          <div class="num">2</div>
          <div class="text">
            <strong>RECHERCHE</strong>
            <br />CRÉE UN ÉVÉNEMENT
          </div>
        </div>
        <div class="troisieme blocchiffretexteetapes">
          <div class="num">3</div>
          <div class="text">
            <strong>RENCONTRE</strong>
            <br />AMUSE TOI
          </div>
        </div>
      </div>
      <br />
      <div class="deuxièmeligne blocchiffretexteetapes">
        <div class="premier">
          <div class="num">1</div>

          <div class="text">
            <strong>INSCRIT TOI</strong>
            <br />CONNECTE TOI
          </div>
        </div>
        <div class="quatrieme blocchiffretexteetapes">
          <div class="num">4</div>

          <div class="text">
            <strong>GARDE CONTACT</strong>
            <br />ET REBELOTE !
          </div>
        </div>
      </div>
    </div>
    <div class="planettournecontainer">
      <img
        class="planetquitourneavecperso"
        style="position: absolute"
        src="@/assets/avecperso.gif"
      />
    </div>
  </div>
</template>

<script>
import degouline from "@/components/degoulinerouge";
import { mapGetters } from "vuex";
import firebase from "firebase";
export default {
  name: "App",
  computed: {
    // map `this.user` to `this.$store.getters.user`
    ...mapGetters({
      user: "user",
    }),
  },
  mounted: function() {
    var d = new Date();
    var day = String(d.getDate()).padStart(2, "0");
    var month = String(d.getMonth() + 1).padStart(2, "0");
    this.placehorlderRecherche.date = day + "/" + month;
    this.placeholderChangement(
      this.placehorlderRechercheListe,
      this.placehorlderRecherche,
      day,
      month
    );
  },
  data: function() {
    return {
      drawer: false,
      group: null,
      act: ["slt", "lol"],
      placehorlderRechercheListe: {
        nom: [
          "Jouer au foot",
          "Faire un basket",
          "Aller au cinéma",
          "Boire une bière",
        ],
        lieux: ["à Grenoble", "à Lyon", "à Paris", "à Montpellier", "à Metz"],
      },
      placehorlderRecherche: {
        nom: "Aller au cinéma",
        lieux: "à Grenoble",
        date: "",
      },
    };
  },
  components: {
    degouline: degouline,
  },
  methods: {
    placeholderChangement(liste, placeholder, day, month) {
      setTimeout(() => {
        var random = Math.floor(Math.random() * liste.nom.length);
        placeholder.nom = liste.nom[random];

        var randomlieux = Math.floor(Math.random() * liste.lieux.length);
        placeholder.lieux = liste.lieux[randomlieux];

        placeholder.date = day + "/" + month;

        if (day < 30) day++;
        else {
          month = month + 1;
          day = 1;
        }

        if (month > 12) {
          month = 0;
        }

        this.placeholderChangement(liste, placeholder, day, month);
      }, 3000);
    },
    signOut() {
      firebase
        .auth()
        .signOut()
        .then(() => {});
    },
  },
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;700&display=swap");
* {
  font-family: "Noto Sans", sans-serif;
}
#app {
  position: relative;
  height: 100vh;
}
body {
  overflow: hidden;
}
#degouline > svg {
  width: 100%;
  height: auto;
}
#degouline {
  width: 101%;
  position: absolute;
}
.title {
  z-index: 1;
}
.planetquitourne {
  margin-top: 5%;
  margin-left: -20%;
  height: 20%;
}

.titrecard {
  margin-top: 10%;
  background-color: transparent !important;
  box-shadow: unset !important;
  text-align: center;

  .v-card__title {
    font-weight: 700;
    justify-content: center;
    color: white;
    padding-bottom: 0 !important;
    font-size: 25px;
  }
  .v-card__text {
    font-family: "Noto Sans", sans-serif;
    opacity: 0.7;
    color: white !important;
    font-size: 12px;
  }
}
.barrederecherchecontainer {
  margin-top: 7vh;
  position: absolute;
  width: 100%;
}
.barrederecherche {
  display: flex;
  justify-content: space-around;
  border-radius: 20px;
  margin: auto;
  background-color: white;
  width: 90%;
  height: 30px;
  box-shadow: 0px 0px 16px -3px rgba(0, 0, 0, 0.25);
  div {
    margin-top: 1%;
  }
}
.comboActivite {
  .v-input__control {
    height: 80% !important;
  }
  .v-input__control > .v-input__slot {
    border-radius: 20px;
    box-shadow: unset !important;
    height: 30px !important;
    min-height: 20px !important;
    width: 50% !important;
    .v-select__slot > .v-input__append-inner {
      visibility: hidden;
    }
    .v-select__slot > label {
      font-size: 8px !important;
      position: unset !important;
      width: 100%;
    }
    .v-select__slot > .v-select__selections > input {
      font-size: 8px;
    }
    .v-select__slot > .v-select__selections > span {
      background-color: white;
      span {
        font-size: 8px;
      }
    }
  }
}
.containerEtapes {
  width: 100%;
  margin-top: 30%;
  position: absolute;
  div > div > .text {
    color: #616a79;
    font-size: 10px;
    opacity: 1;
    position: absolute;
    margin-top: -50px;
    margin-left: 35px;
  }
  .premièreligne {
    width: 100%;
    display: inline-flex;
    justify-content: center;
    div > .num {
      color: #ff0000;
      opacity: 0.23;
      padding: 20px;
      font-size: 50px;
      font-weight: bolder;
    }
    .deuxieme,
    .troisieme {
      margin-right: 15%;
    }
  }
  .deuxièmeligne {
    padding: 20px;
    padding-top: 0 !important;
    width: 100%;
    display: inline-flex;
    justify-content: space-around;
    div > .num {
      color: #ff0000;
      opacity: 0.23;
      padding: 20px;
      font-size: 50px;
      font-weight: bolder;
    }
    .premier,
    .quatrieme {
      margin-right: 30%;
      margin-left: 15%;
    }
  }
}
.planetpersonacceuil {
  margin-top: 50%;
  margin-left: 10% !important;
  width: 90%;
  margin-left: auto;
}
.planetquitourneavecperso {
  width: 100vw;
  left: 50%;
  margin-left: -50vw;
  bottom: 0;
  vertical-align: bottom;
}
.planettournecontainer {
  position: relative;
  bottom: 0;
  margin-top: 190vw;
}
.blocchiffretexteetapes {
  display: block;
}
#inputrechercheevent {
  font-size: 3.5vw;
  width: 18vw;
  transform: translateY(-5px);
}
.nomevent {
}
.pastille {
}
.date {
  width: 16vw !important;
}
.endroit {
  width: 22vw !important;
}
#btncreereventredinterieur {
  margin-top: 5px !important;
}
.titrecarduserheader {
  margin-top: -15px !important;
  div {
    font-size: 5vw !important;
  }
}
</style>
