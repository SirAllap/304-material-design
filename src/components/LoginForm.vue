<template>
  <v-app class="font">
    <v-main>
      <v-container class="mt-5 fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <v-card elevation="12" class="blue-grey darken-3 accent-2">
              <v-window v-model="step">
                <v-window-item :value="2">
                  <v-row
                    ><v-col cols="12" md="7">
                      <v-card-text class="mt-12">
                        <h1 class="text-center teal--text text--accent-2">
                          REBOOT ACADEMY
                        </h1>
                        <v-divider class="mt-3 mb-3" dark></v-divider>
                        <v-form ref="form" v-model="valid" lazy-validation>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            outlined
                            v-model="name"
                            :counter="10"
                            :rules="nameRules"
                            label="Name"
                            prepend-inner-icon="mdi-form-textbox"
                            required
                          ></v-text-field>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            outlined
                            v-model="email"
                            :rules="emailRules"
                            label="E-mail"
                            prepend-inner-icon="mdi-at"
                            required
                          ></v-text-field>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            hint="At least 8 characters"
                            counter
                            :rules="passwordRules"
                            outlined
                            v-model="pass1"
                            :type="passVisible ? 'text' : 'password'"
                            label="Password"
                            prepend-inner-icon="mdi-onepassword"
                            :append-icon="
                              passVisible
                                ? 'mdi-eye-outline'
                                : 'mdi-eye-off-outline'
                            "
                            @click:append="passVisible = !passVisible"
                          ></v-text-field>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            hint="At least 8 characters"
                            counter
                            :rules="[passwordConfirmationRule, passwordRules]"
                            outlined
                            v-model="pass2"
                            :type="passVisible1 ? 'text' : 'password'"
                            label="Confirm password"
                            prepend-inner-icon="mdi-onepassword"
                            :append-icon="
                              passVisible1
                                ? 'mdi-eye-outline'
                                : 'mdi-eye-off-outline'
                            "
                            @click:append="passVisible1 = !passVisible1"
                          ></v-text-field>
                          <v-select
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            outlined
                            v-model="select"
                            label="Country"
                            :rules="[(v) => !!v || 'Item is required']"
                            :items="country"
                            prepend-inner-icon="mdi-select-place"
                            required
                          ></v-select>
                          <v-row>
                            <v-col cols="12" sm="4" md="4">
                              <v-radio-group
                                v-model="radioGroup"
                                dark
                                color="white"
                                :rules="[
                                  (v) => !!v || 'You must choose your gender!',
                                ]"
                              >
                                <template v-slot:label>
                                  <div>Choose <strong>gender:</strong></div>
                                </template>
                                <v-radio
                                  label="Female"
                                  color="red"
                                  value="Female"
                                ></v-radio>
                                <v-radio
                                  label="Male"
                                  color="orange"
                                  value="Male"
                                ></v-radio>
                                <v-radio
                                  label="Undisclosed"
                                  color="success"
                                  value="Undisclosed"
                                ></v-radio>
                              </v-radio-group>
                            </v-col>
                            <v-col cols="12" sm="6" md="6">
                              <v-dialog
                                ref="dialog"
                                v-model="modal"
                                :return-value.sync="date"
                                persistent
                                width="290px"
                              >
                                <template v-slot:activator="{ on, attrs }">
                                  <v-text-field
                                    dark
                                    color="white"
                                    v-model="date"
                                    label="Birthday"
                                    prepend-icon="mdi-cake-variant-outline"
                                    readonly
                                    v-bind="attrs"
                                    v-on="on"
                                  ></v-text-field>
                                </template>
                                <v-date-picker v-model="date" scrollable>
                                  <v-spacer></v-spacer>
                                  <v-btn
                                    text
                                    color="primary"
                                    @click="modal = false"
                                  >
                                    Cancel
                                  </v-btn>
                                  <v-btn
                                    text
                                    color="primary"
                                    @click="$refs.dialog.save(date)"
                                  >
                                    OK
                                  </v-btn>
                                </v-date-picker>
                              </v-dialog>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col cols="12" sm="7" md="7"
                              ><v-checkbox
                                color="white"
                                dark
                                v-model="checkbox"
                                :rules="[
                                  (v) =>
                                    !!v ||
                                    'You must agree the Terms and Conditions to continue!',
                                ]"
                                label="Terms and Conditions"
                                required
                              ></v-checkbox
                            ></v-col>
                            <v-col cols="12" sm="5" md="5"
                              ><v-checkbox
                                color="white"
                                dark
                                label="Mailing List"
                                required
                              ></v-checkbox
                            ></v-col>
                          </v-row>
                          <v-divider dark></v-divider>
                          <v-btn
                            :disabled="!valid"
                            class="mt-5"
                            color="teal accent-2"
                            outlined
                            elevation="2"
                            x-large
                            block
                            @click="validate"
                          >
                            JOIN
                          </v-btn>
                          <v-spacer></v-spacer>
                          <v-btn
                            class="mt-5"
                            color="pink lighten-3"
                            outlined
                            elevation="2"
                            x-large
                            block
                            @click="reset"
                          >
                            clear
                          </v-btn>
                        </v-form>
                      </v-card-text></v-col
                    ><v-col
                      cols="12"
                      md="5"
                      class="alreadyOn deep-purple darken-2"
                    >
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center">Already on Reboot?</h1>
                        <v-divider class="mt-3 mb-3" dark></v-divider>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn
                          class="mt-5"
                          color="teal accent-2"
                          outlined
                          elevation="2"
                          x-large
                          dark
                          @click="step--"
                          >Sign in</v-btn
                        >
                      </div>
                    </v-col>
                  </v-row></v-window-item
                >
                <v-window-item :value="1">
                  <v-row class="fill-height">
                    <v-col cols="12" md="5" class="newTo deep-purple darken-2">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center">New to Reboot?</h1>
                      </v-card-text>
                      <v-divider class="mt-3 mb-3" dark></v-divider>
                      <div class="text-center">
                        <v-btn
                          class="mt-5"
                          color="teal accent-2"
                          outlined
                          elevation="2"
                          x-large
                          dark
                          @click="step++"
                          >Join now</v-btn
                        >
                      </div>
                    </v-col>
                    <v-col cols="12" md="7">
                      <v-card-text class="mt-12">
                        <h1 class="text-center teal--text text--accent-2">
                          Create Account
                        </h1>
                        <v-divider class="mt-3 mb-3" dark></v-divider>
                        <v-form>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            outlined
                            v-model="email"
                            :rules="emailRules"
                            label="E-mail"
                            prepend-inner-icon="mdi-at"
                            required
                          ></v-text-field>
                          <v-text-field
                            background-color="blue-grey darken-2"
                            dark
                            color="white"
                            hint="At least 8 characters"
                            counter
                            :rules="passwordRules"
                            outlined
                            v-model="pass1"
                            :type="passVisible ? 'text' : 'password'"
                            label="Password"
                            prepend-inner-icon="mdi-onepassword"
                            :append-icon="
                              passVisible
                                ? 'mdi-eye-outline'
                                : 'mdi-eye-off-outline'
                            "
                            @click:append="passVisible = !passVisible"
                          ></v-text-field>
                          <v-divider class="mt-3 mb-3" dark></v-divider>
                          <div class="text-center mt-5">
                            <v-btn
                              class="mt-5"
                              color="teal accent-2"
                              outlined
                              elevation="2"
                              x-large
                              block
                            >
                              sign in
                            </v-btn>
                          </div>
                        </v-form>
                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
              <v-alert
                :class="{ alert: alert, 'text-success': noError }"
                dismissible
                outlined
                prominent
                type="success"
                >You have successfully registered</v-alert
              >
              <v-alert
                :class="{ alert: alert, 'text-danger': hasError }"
                color="red"
                dismissible
                outlined
                prominent
                type="error"
                >Something went wrong</v-alert
              >
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { countries } from "@/assets/countries.js";

export default {
  data: () => ({
    step: 1,
    valid: true,
    name: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 10) || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    select: null,
    country: [],
    checkbox: false,
    pass1: "",
    pass2: "",
    passwordRules: [
      (v) => !!v || "Required.",
      (v) => v.length >= 8 || "Min 8 characters",
    ],
    radioGroup: "",
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu: false,
    modal: false,
    menu2: false,
    passVisible: false,
    passVisible1: false,
    alert: true,
    noError: true,
    hasError: true,
  }),
  props: {
    source: String,
  },
  mounted() {
    countries.forEach((e) => this.country.push(e.name));
  },
  computed: {
    passwordConfirmationRule() {
      return () => this.pass1 === this.pass2 || "Password must match";
    },
  },

  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
  },
};
</script>

<style scoped>
.font {
  font-family: "Cormorant", serif;
}
h1 {
  font-size: calc(1vw + 1vh + 2.5vmin);
}
.newTo {
  background-image: url("https://images.pexels.com/photos/1072179/pexels-photo-1072179.jpeg?cs=srgb&dl=pexels-c%C3%A1tia-matos-1072179.jpg&fm=jpg");
  background-size: 1000px 1000px;
}
.alreadyOn {
  background-image: url("https://images.pexels.com/photos/1072179/pexels-photo-1072179.jpeg?cs=srgb&dl=pexels-c%C3%A1tia-matos-1072179.jpg&fm=jpg");
  background-size: 1000px 1000px;
}
.alert {
  width: 70%;
  margin: 10px auto;
}
.text-success {
  display: none;
}
.text-danger {
  display: none;
}
</style>
