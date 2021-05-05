<template>
  <div class="card mx-auto">
    <div class="card-body">
      <h5 class="card-title">insert your data in the form please</h5>
      <h6 class="card-subtitle mb-2 text-muted">remember that the fields with * are required</h6>
      <form id="form" @submit.prevent="send">
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
            <input type="number" class="form-control" id="age" min="18" max="99" maxlength="2"
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
        <div class="form-group row" v-for="(ph, index) in cv.phone" v-bind:key="ph">
          <strong class="col-sm-2 col-form-label"><label for="phone">
            Phone {{index + 1}}
            <label class="required">*</label>
          </label> </strong>
          <div class="col-sm-6">
            <input type="tel" id="phone" class="form-control" maxlength="10"
                   placeholder="3xx xxx xx xx" autocomplete="off" v-model="ph.number" required>
          </div>
          <strong class="col-sm-2">
                <span class="close" @click="addPhone"
                      title="add Phone">
                  <img src="@/assets/addicon.png" style="max-height: 30px; max-width: 30px">
                </span>
          </strong>
          <strong class="col-sm-2">
                <span class="close" @click="deletePhone(index)"
                      title="add Phone" v-if="isPhclose">
                  <img src="@/assets/deleteicon.png" style="max-height: 30px; max-width: 30px">
                </span>
          </strong>
        </div>
        <hr>
        <h5 class="card-title" style="margin-top: 1em;">Education</h5>
        <div class="card" v-for="(edu, index) in cv.education" v-bind:key="edu">
          <div class="card-body">
            <h6 class="card-subtitle mb-2 text-muted">Site {{ index + 1 }}</h6>
            <div class="form-group row">
              <strong class="col-sm-2 col-form-label"><label for="name">
                Name
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-8">
                <input type="text" id="eduplace" class="form-control"
                       placeholder="University" autocomplete="off" v-model="edu.place" required>
              </div>
              <strong class="col-sm-2">
                <span class="close" @click="deleteEducation(index)"
                      title="Delete Education" v-if="isclose">
                  <img src="@/assets/deleteicon.png" style="max-height: 30px; max-width: 30px">
                </span>
              </strong>
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
              <strong class="col-sm-2 col-form-label" v-if="!edu.isfinish"><label for="name">
                End Date
                <label class="required">*</label>
              </label> </strong>
              <div class="col-sm-3" v-if="!edu.isfinish">
                <input type="date" id="eduenddate" class="form-control"
                       placeholder="University" autocomplete="off" v-model="edu.enddate" required>
              </div>
              <div class="col-sm-1">
                <div class="form-check">
                  <input class="form-check-input" type="checkbox" value=""
                         id="notfinish" v-model="edu.isfinish">
                  <label class="form-check-label" for="notfinish">
                    Not Finish
                  </label>
                </div>
              </div>
              <strong class="col-sm-1 col-form-label"><label style="cursor: pointer"
                        title="Add Education" @click="addEducation">
                <img src="@/assets/addicon.png" style="max-height: 30px; max-width: 30px">
              </label> </strong>
            </div>
          </div>
        </div>
        <div class="alert alert-success" role="alert" v-if="sent">
          <h4 class="alert-heading">Ready!</h4>
          <label>We haver your data now</label> <br>
          <label class="mb-0">We will get in contact as soon as possible.</label>
        </div>
        <button type="submit" class="btn btn-primary" id="enviar">Send</button>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'MyForm',
  data() {
    return {
      isclose: false,
      isPhclose: false,
      sent: false,
      cv: {
        name: null,
        age: null,
        gender: null,
        email: null,
        phone: [
          {
            number: null,
          },
        ],
        education: [
          {
            place: null,
            type: null,
            course: null,
            startdate: null,
            enddate: null,
            isfinish: false,
          },
        ],
      },
    };
  },
  watch: {
    sent(val) {
      setTimeout(() => {
        if (val) this.sent = false;
      }, 3000);
    },
  },
  methods: {
    send() {
      this.isclose = false;
      this.sent = true;
    },
    addEducation() {
      this.cv.education.push({
        place: null,
        type: null,
        course: null,
        startdate: null,
        enddate: null,
      });
      this.isclose = true;
    },
    deleteEducation(index) {
      this.cv.education.splice(index, 1);
      if (this.cv.education.length === 1) {
        this.isclose = false;
      }
    },
    addPhone() {
      this.cv.phone.push({
        number: null,
      });
      this.isPhclose = true;
    },
    deletePhone(index) {
      this.cv.phone.splice(index, 1);
      if (this.cv.phone.length === 1) {
        this.isPhclose = false;
      }
    },
  },
};
</script>

<style src="../store/StyleForm.css" type="text/css"/>
