<template>
  <div class="container">
      <form  @submit.prevent="login">
          <div>
            <div class="form-group">
                <input v-model="userData.username" id="username" class="form-control" type="text" placeholder="Username">
            </div>
            <div class="form-group">
                <input v-model="userData.password" id="password" class="form-control" type="text" placeholder="Password">
            </div>
            <div class="form-group">
                <div class="checkbox">
                    <input class="form-control" type="checkbox" id="remember" name="remember" />
                    <label for="remember">Remember Me</label>
                </div>
            </div>
            <div class="form-group submit">
                <button class="button">Login</button>
            </div>
          </div>
      </form>
  </div>
</template>

<script>
  export default {
      name: 'login',
      data() {
          return {
              userData: {
                  username: 'test',
                  password: 'test'
              }
          }
      },
      methods: {
          async login() {
              // await this.$auth.loginWith("local", {
              //     data: this.userData
              // }).then((response) => {
                  // if (response.status === 200) {
                      // this.$router.go("/home")
                      if(this.userData.username =='test' && this.userData.password == 'test'){
                        this.$router.push('/home')
                      } else {
                        alert("Invalid Login Details")                        
                      }
                  // }
              // }).catch((error) => {
              //     throw new Error(error)
              // })
          }
      },
  }
</script>
<style>

input[type=text], input[type=password] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.button {
  background-color: #04AA6D;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}

.button:hover {
  opacity: 0.8;
}

.cancelbtn {
  width: auto;
  padding: 10px 18px;
  background-color: #f44336;
}

.imgcontainer {
  text-align: center;
  margin: 24px 0 12px 0;
}

img.avatar {
  width: 40%;
  border-radius: 50%;
}

.container {
  padding: 16px;
}

span.psw {
  float: right;
  padding-top: 16px;
}

/* Change styles for span and cancel button on extra small screens */
@media screen and (max-width: 300px) {
  span.psw {
     display: block;
     float: none;
  }
  .cancelbtn {
     width: 100%;
  }
}
</style>