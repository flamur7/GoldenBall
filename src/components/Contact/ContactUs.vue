<template>
  <section>
    <div class="container-fluid py-5">
      <div class="row d-flex">
        <div class="col-12 col-xl-6 col-lg-6 col-md-6 col-sm-12 order-sm-0 order-12" style="margin-right:-150px;">
          <img class="img-fluid" src="@/assets/bg1.jpg" style="height: 75.5%;">
        </div>
        <div class="col-12 col-xl-6 col-lg-5 col-md-6 col-sm-12 order-first order-xl-0">
          <h1>Hello, Football Fan</h1>
          <h2 style="color:grey">got a thought to discuss?</h2>
          <form style="text-align: -webkit-left;" @submit.prevent="createContact">
            <div class="form-group">
              <input v-model="form.name" type="text" class="form-control" style="color:black; text-indent: 120px;" required>
              <label class="label" for="name" style="color:white"><b>Name</b></label>
            </div>
            <div class="form-group">
              <input v-model="form.email" type="email" class="form-control" style="color:black; text-indent: 120px;" required>
              <label class="label" for="E-mail" style="color:white"><b>E-mail</b></label>
            </div>
            <div class="form-group">
              <textarea v-model="form.message" class="form-control" id="texting" style="overflow:hidden; text-indent: 120px; height:130px; color:black;"  required></textarea>
              <label class="label" for="Message" style="color:white"><b>Message</b></label>
            </div>
              <button type="submit" class="btn btn-light" href="#" style="background-color:black; color:white" role="button">Submit</button>
          </form>
        </div>
        </div>
      </div>
  </section>
</template>

<script>
import apiRequest from "../../utility/apiRequest";
export default {
  name: 'ContactUs',
  data(){
    return {
      form:{
        name: "",
        email: "",
        message:"",
      },
      error: null,
    };
  },
  methods: {
    async createContact() {
      await apiRequest.createContact({ ...this.form });
      this.$router.replace({ name: "Home"});
    },
  },
};
</script>

<style scoped>
#texting{
  text-indent: 110px;
}


form {
  width: 100%;
  padding: 50px 0;
  display: block;
  margin: 0 auto;
}

.form-group {
  width: 100%;
  position: relative;
  margin: 0 0 50px;
}
.form-group label {
  font-weight: 100;
  font-size: 1.5rem;
  color: grey;
  position: absolute;
  transition: .5s ease-in-out;
  top: 0px;
  z-index: 0;
}
.form-group input, .form-group textarea  {
  outline: none;
  box-shadow: none;
  background-color: transparent;
  border: 0;
  border-bottom: 1px solid #555;
  font-size: 1.4rem;
  font-weight: 100;
  width: 100%;
  height: 40px;
  transition: all 0.5s;
  z-index: 1;
  position: relative;
  border-radius: 0;
  resize: none;
  scroll-behavior: none;
}

.form-group input:valid ~ label,
.form-group input:focus ~ label,
.form-group textarea:valid ~ label,
.form-group textarea:focus ~ label {
  color: #71acd6;
  font-size: 1rem;
  top: -15px;
  transition: all 0.5s;
}

.form-group input:valid,
.form-group input:focus,
.form-group textarea:valid,
.form-group textarea:focus{
  border-color: #71acd6;
}

form button {
  -webkit-transition-duration: 200ms;
  transition-duration: 200ms;
  width: 120px;
  height: 50px;
  font-size: 15px;
  padding: 0px 30px;
  cursor: pointer;
  box-shadow: 0 26px 38px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

</style>
