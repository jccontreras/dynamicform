<template>
  <div class="card mx-auto">
    <div class="card-body">
      <h5 class="card-title">insert your data in the form please</h5>
      <h6 class="card-subtitle mb-2 text-muted">remember that the fields with * are required</h6>
      <form id="form">
        <h5 class="card-title" style="margin-top: 1em;">Personal Info</h5>
        <div class="form-group row">
          <strong class="col-sm-2 col-form-label"><label for="name">
            Full Name
            <label class="required">*</label>
          </label> </strong>
          <div class="col-sm-10">
            <input type="text" id="name" class="form-control"
                   placeholder="full name" autocomplete="off" v-model="cv.name" required>
          </div>
        </div>
        <div class="form-group row">
          <strong class="col-sm-2 col-form-label"><label for="age">
            Age
            <label class="required">*</label>
          </label></strong>
          <div class="col-sm-4">
            <input type="number" class="form-control" id="age" min="18" max="99"
                   v-model="cv.age">
          </div>
          <strong class="col-sm-2 col-form-label"><label for="radio1">Gender</label></strong>
          <div class="col-sm-4">
            <div class="custom-control custom-radio">
              <input type="radio" class="custom-control-input" value="F"
                     id="radio1" name="groupOfDefaultRadios" v-model="cv.gender">
              <label class="custom-control-label" for="radio1">Female</label>
            </div>
            <div class="custom-control custom-radio">
              <input type="radio" class="custom-control-input" value="M"
                     id="radio2" name="groupOfDefaultRadios" v-model="cv.gender">
              <label class="custom-control-label" for="radio2">Male</label>
            </div>
          </div>
        </div>
        <div class="form-group row">
          <strong class="col-sm-2 col-form-label"><label for="name">
            E-mail
            <label class="required">*</label>
          </label> </strong>
          <div class="col-sm-10">
            <input type="email" id="email" class="form-control"
                   placeholder="example@somthing.x" autocomplete="off" v-model="cv.email" required>
          </div>
        </div>
        <h5 class="card-title" style="margin-top: 1em;">Education</h5>
        <div class="card" v-for="(edu, index) in cv.education" v-bind:key="edu">
          <div class="card-body">
            <span class="close" @click="deleteEducation(index)">x</span>
            <h6 class="card-subtitle mb-2 text-muted site">Site {{ index + 1 }}</h6>
            <div class="form-group row">
              <strong class="col-sm-2 col-form-label"><label for="name">
                Name
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-10">
                <input type="text" id="eduplace" class="form-control"
                       placeholder="University" autocomplete="off" v-model="edu.place" required>
              </div>
            </div>
            <div class="form-group row">
              <strong class="col-sm-2 col-form-label"><label for="name">
                Type of Education
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-3">
                <select class="custom-select" id="edutype" v-model="edu.type" required>
                  <option selected>Choose...</option>
                  <option value="1">High School</option>
                  <option value="2">Technique</option>
                  <option value="3">Technological</option>
                  <option value="4">University</option>
                  <option value="5">Specialization</option>
                  <option value="6">Master's degree</option>
                  <option value="7">PhD</option>
                </select>
              </div>
              <strong class="col-sm-2 col-form-label"><label for="name">
                Name
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-5">
                <input type="text" id="educourse" class="form-control"
                       placeholder="Course name" autocomplete="off" v-model="edu.course" required>
              </div>
            </div>
            <div class="form-group row">
              <strong class="col-sm-2 col-form-label"><label for="name">
                Start Date
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-3">
                <input type="date" id="edustartdate" class="form-control"
                       placeholder="University" autocomplete="off" v-model="edu.startdate" required>
              </div>
              <strong class="col-sm-2 col-form-label"><label for="name">
                End Date
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-3">
                <input type="date" id="eduenddate" class="form-control"
                       placeholder="University" autocomplete="off" v-model="edu.enddate" required>
              </div>
              <strong class="col-sm-2 col-form-label"><label style="cursor: pointer"
              title="Add Education" @click="addEducation">
                +
              </label> </strong>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'MyForm',
  data() {
    return {
      cv: {
        name: null,
        age: null,
        gender: null,
        email: null,
        education: [
          {
            place: null,
            type: null,
            course: null,
            startdate: null,
            enddate: null,
          },
        ],
      },
    };
  },
  methods: {
    send() {
      alert('Se envio correctament el formulario');
    },
    addEducation() {
      this.cv.education.push({
        place: null,
        type: null,
        course: null,
        startdate: null,
        enddate: null,
      });
    },
    deleteEducation(index) {
      this.cv.education.splice(index, 1);
    },
  },
};
</script>

<style>
.card {
  margin-top: 2em;
  background-color: whitesmoke;
  max-width: 50rem;
}

.required {
  color: red;
}

#form {
  margin-top: 2em;
}

.form-group {
  margin-top: 1em;
}

.custom-control-label {
  margin-left: 1em;
}

.close {
  cursor: pointer;
  margin-left: 45rem;
  margin-top: 1rem;
}

.site {
  margin-right: 40rem;
}
</style>
