<template>
  <div>
    <div class="sidenav">
      <div class="login-main-text">
        <h2>
          Sprint 3<br />
          Grupo 1
        </h2>
        <p>UTP - MISIÓN TIC 2022</p>
      </div>
    </div>
    <div class="main">
      <div class="col-md-6 col-sm-12">
        <div class="login-form">
          <form>
            <div class="form-group">
              <h3>
                <label
                  >Hola, {{ user.username }}<br />
                  bienvenido
                </label>
              </h3>
            </div>
            <div class="form-group">
              <p>
                <label>Su correo es {{ user.email }}<br /> </label>
              </p>
            </div>
          </form>
          <button @click.prevent="logOut()" type="submit" class="btn btn-black">
            Logout
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import swal from "sweetalert";
import VueJwtDecode from "vue-jwt-decode";
export default {
  data() {
    return {};
  },
  methods: {
    getUserDetails() {
      let token = localStorage.getItem("jwt");
      let user = VueJwtDecode.decode(token);

      if (token) {
        this.user = user;
      }
    },
    logOut() {
      swal("Gracias por visitarnos", "Vuelve pronto");
      localStorage.removeItem("jwt");
      localStorage.removeItem("user");
      this.$router.push("/");
    },
  },
  created() {
    this.getUserDetails();
  },
};
</script>
<style scoped>
body {
  font-family: "Lato", sans-serif;
}

.main-head {
  height: 150px;
  background: #fff;
}

.sidenav {
  height: 100%;
  background-color: #000;
  overflow-x: hidden;
  padding-top: 20px;
}

.main {
  padding: 0px 10px;
}

@media screen and (max-height: 450px) {
  .sidenav {
    padding-top: 15px;
  }
}

@media screen and (max-width: 450px) {
  .login-form {
    margin-top: 10%;
  }

  .register-form {
    margin-top: 10%;
  }
}

@media screen and (min-width: 768px) {
  .main {
    margin-left: 40%;
  }

  .sidenav {
    width: 40%;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
  }

  .login-form {
    margin-top: 80%;
  }

  .register-form {
    margin-top: 20%;
  }
}

.login-main-text {
  margin-top: 20%;
  padding: 60px;
  color: #fff;
}

.login-main-text h2 {
  font-weight: 300;
}

.btn-black {
  background-color: #000 !important;
  color: #fff;
}
</style>
