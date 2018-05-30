<template>
  <form>
    <v-layout row>
    <v-text-field
      v-validate="'required'"
      v-model="course.label"
      :error-messages="errors.collect('label')"
      label="Label"
      data-vv-name="label"
      required
      autofocus
    ></v-text-field>
    <span>&nbsp;&nbsp;&nbsp;</span>
    <v-text-field
      v-validate="'required'"
      v-model="course.title"
      :error-messages="errors.collect('title')"
      label="Title"
      data-vv-name="title"
      required
    ></v-text-field>
    </v-layout>
    <v-text-field
      v-validate="'required'"
      v-model="course.description"
      :error-messages="errors.collect('description')"
      label="Description"
      data-vv-name="description"
      required
    ></v-text-field>
    <v-menu
      ref="dateMenu"
      :close-on-content-click="false"
      v-model="dateMenu"
      :nudge-right="40"
      lazy
      transition="scale-transition"
      offset-y
      full-width
      max-width="290px"
      min-width="290px"
    >
      <v-text-field
        v-validate="'required'"
        slot="activator"
        v-model="course.date"
        :error-messages="errors.collect('date')"
        label="Date"
        hint="YYYY-MM-DD format"
        persistent-hint
        prepend-icon="event"
        readonly
        data-vv-name="date"
        required
      />
      <v-date-picker
        v-model="course.date"
        no-title
        @input="dateMenu = false"/>
    </v-menu>

    <v-btn @click="submit">submit</v-btn>
    <v-btn @click="clear">clear</v-btn>
  </form>
</template>

<script>
import { Course } from 'Models/course.model';
  export default {
    name: 'ClassroomForm',
    data: () => ({
      course: new Course(),
      dateMenu: false,
    }),

    methods: {
      submit () {
        this.$validator.validateAll();
      },
      clear () {
        this.course = new Course();
        this.$validator.reset();
      },
    },
  };
</script>