<template>
  <div id="employee-form">
		<b-form @submit.prevent="handleSubmit">
			<b-form-group
				label="Employee Name"
				label-for="input-group-employee-name"
				description="Name and surname"
			>
				<b-form-input
					id="input-group-employee-name"
					ref="first"
					type="text"
					:class="{ 'has-error': submitting && invalidName }"
					v-model="employee.name"
					placeholder="Enter name"
					@focus="clearStatus"
					@keypress="clearStatus"
				/>
			</b-form-group>

			<b-form-group
				label="Employee Email"
				label-for="input-group-employee-email"
				description="Email address"
			>
				<b-form-input
				type="email"
				required
				placeholder="Enter email"
				:class="{ 'has-error': submitting && invalidEmail }"
				v-model="employee.email"
				@focus="clearStatus"
				/>
			</b-form-group>
			
			<p v-if="error && submitting" class="error-message">
				❗Please fill out all required fields
			</p>
			<p v-if="success" class="success-message">
				✅ Employee successfully added
			</p>

			<b-button type="submit" variant="primary">Add Employee</b-button>
		</b-form>
  </div>
</template>

<script>
  export default {
		name: 'employee-form',
		
		data() {
			return {
				submitting: false,
				error: false,
				success: false,
				employee: {
					name: '',
					email: '',
				},
			}
		},

		methods: {
			handleSubmit() {
				this.submitting = true
				this.clearStatus()

				if (this.invalidName || this.invalidEmail) {
					this.error = true
					return
				}

				this.$emit('add:employee', this.employee)
				this.$refs.first.focus()

				this.employee = {
					name: '',
					email: '',
				}
				this.error = false
				this.success = true
				this.submitting = false
			},

			clearStatus() {
				this.success = false
				this.error = false
			}		
		},

		computed: {
			invalidName() {
				return this.employee.name === ''
			},

			invalidEmail() {
				return this.employee.email === ''
			},
		}
  }
</script>

<style scoped>
  form {
		margin-bottom: 2rem;
  }

	[class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>