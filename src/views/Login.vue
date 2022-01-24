
<template>
	<v-card width="600" class="mx-auto mt-15 card-color" elevation="2">
		<v-card-title>
      <div class="login-text-line">
			<h1 class="display-1 login-text">Login
        <span class="border-line"></span>
      </h1>
      </div>
		</v-card-title>
		<v-card-text>
          <ValidationObserver ref="loginForm" v-slot="{handleSubmit}">
			<v-form @submit.stop.prevent="handleSubmit(login)">
                <ValidationProvider v-slot="{ errors }" name="User ID" :rules="{ required: true }">
                  <v-text-field outlined label="User ID" :error-messages="errors" v-model="email"></v-text-field>
                </ValidationProvider>
                <ValidationProvider v-slot="{ errors }" name="Password" :rules="{required: true}">
                  <v-text-field
                  outlined
						:type="showPassword ? 'text' : 'password'"
						label="Password"
                        v-model="password"
						
						:append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
						@click:append="showPassword = !showPassword"
                        :error-messages="errors"
					/>
                </ValidationProvider>
                <span class="forget-password">Forget Password?</span>
          <div class="sign-up-account">
            <span class="not-account">Don't have an account?</span>
            <span class="sign-up">SIGN UP</span> 
          </div>
				<v-card-actions>
            <v-btn x-large type="submit" color="default" class="sign-in">
                        SIGN IN
                    </v-btn>
				</v-card-actions>
			</v-form>
          </ValidationObserver>
		</v-card-text>
		</v-card>
</template>

<script>
export default {
    name: 'Login',
    data(){
        return{
            email: '',
            password: '',
            showPassword: false,
            loading: false,
            errors: ''
        }
    },
    methods: {
        login(){
            this.errors = ""
                 const notification = {
                  type:'success',
                  message: "LoggedIN Successfully"
                }
                this.$store.dispatch('add',notification)
        }
    }
}
</script>

<style lang="scss" scoped>
div{
  &.login-text-line{
    position: relative;
  }
  h1{
    &.login-text{
      color: white;
      font-size: 12px;
    }
  }
}
span{
  &.border-line{
    border-bottom: 2px solid brown;
    position: absolute;
  }
}
span{
  &.forget-password{
    font-weight: 500;
    color: white;
    margin-left: 12px;
  }
}
div{
  &.sign-up-account{
    display: flex;
    justify-content: space-between;
    margin-top: 30px;
  }
  span{
    &.sign-up{
      font-weight: 500;
      color: white;
      margin-right: 8px;
    }
  }
  span{
    &.not-account{
      color: white;
      margin-left: 12px;
    }
  }
}
    .sign-in{
      color: black;
      width: 560px;
    }
.card-color{
  background-color: #10578f !important;
}
</style>