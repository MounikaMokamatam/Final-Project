<script setup lang="ts">
import { ref } from 'vue';
import router from '../router';
import { useSession } from '../models/session';
const session = useSession();
const firstName = ref('');
const lastName = ref('');
const username = ref('');
const password = ref('');
const confirm = ref('');
const error = ref('error');
const errorText = ref('');

const signup = () => {
	if(firstName.value === "" || lastName.value === "" ||username.value === "" || password.value === "" || confirm.value === "") {
		errorText.value = "Some fields are empty";
		return;
	}
	if(password.value !== confirm.value) {
		errorText.value = "Passwords don't match"; 
		error.value = 'error visible'
		return;
	}
	const { floor, random } = Math;
	const n = floor(random() * 100);

	console.log('Registering');
	session.SignUp('Wilson', 'Chola','handlee', password.value,username.value, `https://randomuser.me/api/portraits/men/${n}.jpg`, 10);
	console.log('Registered user haha');
	/*
	User.push({
		username: username.value,
		password: password.value,
		avatar: `https://randomuser.me/api/portraits/men/${n}.jpg`
	});
	*/
	router.push("./login");
	error.value = 'error';
}
</script>

<template>

	<div class="section">

        <div class="columns">
            <div class="column is-half is-offset-one-quarter">
                <div class="card">
					<div class="card-content">
						<div class="content">
							<h3 class="">Sign up page</h3>
							<form  @submit.prevent="login">

								<div class="field">
									<p class="control has-icons-left">
									<input type="text" class="input" name="firstName" required placeholder="firstName" v-model="firstName">
										<span class="icon is-small is-left">
											<i class="fa-solid fa-user"></i>
										</span>
									</p>
								</div>

								<div class="field">
									<p class="control has-icons-left">
									<input type="text" class="input" name="lastName" required placeholder="lastName" v-model="lastName">
										<span class="icon is-small is-left">
											<i class="fa-solid fa-user"></i>
										</span>
									</p>
								</div>
								
								<div class="field">
									<p class="control has-icons-left">
									<input type="text" class="input" name="username" required placeholder="Username" v-model="username">
										<span class="icon is-small is-left">
											<i class="fa-solid fa-user"></i>
										</span>
									</p>
								</div>
								<div class="field">
									<p class="control has-icons-left">
									<input type="password" class="input" name="password" required placeholder="Password" v-model="password">
										<span class="icon is-small is-left">
											<i class="fa-solid fa-key"></i>
										</span>
									</p>
								</div>

								<div class="field">
									<p class="control has-icons-left">
									<input type="password" class="input" name="password" required placeholder="Confirm" v-model="confirm">
										<span class="icon is-small is-left">
											<i class="fa-solid fa-key"></i>
										</span>
									</p>
								</div>

								<div class="field">
									<p class="control">
										<button class="button is-success" type="button" @click="signup">
											<span class="icon is-small">
												<i class="fa-solid fa-user-plus"></i>
											</span>
											<span>Sign Up</span>
										</button>
									</p>
								</div>
								<div v-if="errorText" class="notification is-danger">
									<button class="delete"></button>
									{{errorText}}
								</div>
							</form>
						</div>
					</div>
                </div>
            </div>
        </div>
    </div>
	
</template>

<style lang="scss" scoped>
.error {
	color: red;
	position: absolute;
	top: 76%;
	right: 24%;
	display: none;
}
.visible {
	display: unset;
}
.title {
	position: absolute;
	top: 27%;
	transform: translate(-50%, -50%);
	right: 19%;
	font-size: 48px;
}
.btns {
	display: flex;
	flex-direction: column;
	position: absolute;
	top: 60%;
	transform: translate(-50%, -50%);
	right: 15%;
	button, input {
		width: 250px;
		margin-bottom: 30px;
	}
}
.ill {
	position: absolute;
	width: 700px;
	top: 50%;
	transform: translateY(-50%);
	left: 10%;
}

</style>