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
              <label>Correo electronico</label>
              <input
                v-model="login.email"
                type="email"
                class="form-control"
                placeholder="User Name"
              />
            </div>
            <div class="form-group">
              <label>Password</label>
              <input
                v-model="login.password"
                type="password"
                class="form-control"
                placeholder="Password"
              />
            </div>
            <button
              @click.prevent="loginUser()"
              type="submit"
              class="btn btn-black"
            >
              Login
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import swal from "sweetalert";
export default {
  name: "TheLogin",
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        let response = await this.$http.post("/api/user/login", this.login);
        console.log(response.data);
        let token = response.data.tokenReturn;
        let user = response.data.user;

        localStorage.setItem("jwt", token);
        localStorage.setItem("user", JSON.stringify(user));
        if (token) {
          swal("Muy bien", "Haz ingresado", "success");
          this.$router.push("/home");
        }
      } catch (e) {
        swal("Ohhhhh noooo!!!", "Revisa tus credenciales", "error");
      }
    },
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
