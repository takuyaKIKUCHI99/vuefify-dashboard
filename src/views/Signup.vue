<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup Page</h1>
        <v-form>
          <v-text-field label="Email" type="email" />
          <v-autocomplete label="Which browser do you use?" :items="browsers" />
          <v-file-input label="Attach profile picture" />

          <!-- Birthday -->
          <v-menu
            v-model="birthdayMenu"
            :close-on-content-click="false"
            :nudge-right="40"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                v-model="birthday"
                label="Birthday"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="birthday" @input="birthdayMenu = false"></v-date-picker>
          </v-menu>

          <v-checkbox label="Agree to terms & conditions" />
          <v-btn type="submit" color="primary">Submit</v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Signup",
  data() {
    return {
      date: new Date().toISOString().substr(0, 10),
      birthday: "",
      birthdayMenu: false,
      browsers: ["Chrome", "Firefox", "Safari", "Edge", "Brave"],
    };
  },
};
</script>