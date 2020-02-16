<template>
	<div class="container">
		<div class="z-depth-1 grey lighten-4 row"
		     style="display: inline-block; padding: 32px 48px 0px 48px; border: 1px solid #EEE;">

			<form class="col s12">
				<div class='row'>
					<div class='col s12'>
						<h5 class="indigo-text">Log In</h5>
					</div>
				</div>

				<div class='row'>
					<div class='input-field col s12'>
						<i class="material-icons prefix">email</i>
						<input v-model="email" id="email" type="email" name="email" required/>
						<label for='email'>Enter your email</label>
					</div>
				</div>

				<div class='row'>
					<div class='input-field col s12'>
						<i class="material-icons prefix">lock</i>
						<input v-model="password" id="pass" type="password" name="password" required/>
						<label for='pass'>Enter your password</label>
					</div>
				</div>

				<br/>
				<div style="text-align: center;">
					<div class='row'>
						<button type='submit' v-on:click="login" class='col s12 btn btn-medium waves-effect indigo'>
							Login
						</button>
					</div>
				</div>
			</form>
		</div>
	</div>
</template>

<script>
	import firebase from "firebase";

	export default {
		name: 'login',
		data() {
			return {
				email: '',
				password: ''
			}
		},
		methods: {
			login: function (e) {

				firebase.auth().signInWithEmailAndPassword(this.email, this.password)
					.then(user => {
						alert(`You are logged in as ${user.user.email}`);
						this.$router.go(this.$router.path);
					}, err => {
						alert(err.message);
					});

				e.preventDefault();
			}
		}
	}
</script>

<style scoped>

	.input-field input[type=date]:focus + label,
	.input-field input[type=text]:focus + label,
	.input-field input[type=email]:focus + label,
	.input-field input[type=password]:focus + label {
		color: #e91e63;
	}

	.input-field input[type=date]:focus,
	.input-field input[type=text]:focus,
	.input-field input[type=email]:focus,
	.input-field input[type=password]:focus {
		border-bottom: 2px solid #e91e63;
		box-shadow: none;
	}
</style>