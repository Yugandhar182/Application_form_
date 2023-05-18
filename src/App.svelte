<script>
  import { createEventDispatcher } from 'svelte';
  import 'bootstrap/dist/js/bootstrap.min.js';

  

  const dispatch = createEventDispatcher();

  let firstName = '';
  let surname = '';
  let email = '';
  let password = '';
  let mobile = '';

  let errors = {
    firstName: '',
    surname: '',
    email: '',
    password: '',
    mobile: ''
  };

  let submissionStatus = '';
  let submissionData = {};

  const validateForm = () => {
    let valid = true;
    errors = {
      firstName: '',
      surname: '',
      email: '',
      password: '',
      mobile: ''
    };

    // Validate First Name
    if (firstName.length === 0) {
      errors.firstName = 'First Name is required';
      valid = false;
    } else if (firstName.length > 28) {
      errors.firstName = 'First Name cannot exceed 28 characters';
      valid = false;
    }

    // Validate Surname
    if (surname.length === 0) {
      errors.surname = 'Surname is required';
      valid = false;
    } else if (surname.length > 28) {
      errors.surname = 'Surname cannot exceed 28 characters';
      valid = false;
    }

 
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (email.length === 0) {
      errors.email = 'Email is required';
      valid = false;                                     // Validate Email (const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;)
    } else if (!emailRegex.test(email)) {
      errors.email = 'Invalid email format';
      valid = false;
    }
    

    //To Validate Password we use (const passwordRegex = /^(?=.*[A-Za-z0-9])(?=.*[!@#$%^&*()])[A-Za-z0-9!@#$%^&*()]{6,15}$/;)
    const passwordRegex = /^(?=.*[A-Za-z0-9])(?=.*[!@#$%^&*()])[A-Za-z0-9!@#$%^&*()]{6,15}$/;
    if (password.length === 0) {
      errors.password = 'Password is required';                 
      valid = false;
    } else if (!passwordRegex.test(password)) {
      errors.password = 'Your password must have at least eight characters long, one uppercase, one lowercase character, and one number';
      valid = false;
    }

  
    const mobileRegex = /^[0-9+]+$/;
    if (mobile.length === 0) {                    //  To Validate Mobile we use this (const mobileRegex = /^[0-9+]+$/;)
      errors.mobile = 'Mobile is required';
      valid = false;
    } else if (!mobileRegex.test(mobile)) {
      errors.mobile = 'Mobile Number is incorrect format';
      valid = false;
    }

    if (valid) {
      // Submit the form
      submissionStatus = 'success';
      submissionData = {
        firstName,
        surname,
        email,
        password,
        mobile
      };
      dispatch('submit', submissionData);
    }
  };
</script>



<form on:submit|preventDefault={validateForm}>
  <div>
    <label for="firstName">First Name:</label>
    <input type="text" id="firstName" bind:value={firstName} />
    {#if errors.firstName}
      <p class="error">{errors.firstName}</p>
    {/if}
  </div>

  <div>
    <label for="surname">Surname:</label>
    <input type="text" id="surname" bind:value={surname} />
    {#if errors.surname}
      <p class="error">{errors.surname}</p>
    {/if}
  </div>

  <div>
    <label for="email">Email:</label>
    <input type="email" id="email" bind:value={email} />
    {#if errors.email}
      <p class="error">{errors.email}</p>
    {/if}
  </div>

  <div>
    <label for="password">Password:</label>
    <input type="password" id="password" bind:value={password} />
    {#if errors.password}
      <p class="error">{errors.password}</p>
    {/if}
  </div>

  <div>
    <label for="mobile">Mobile:</label>
    <input type="text" id="mobile" bind:value={mobile} />
    {#if errors.mobile}
      <p class="error">{errors.mobile}</p>
    {/if}
  </div>

  <button type="submit">Submit</button>
</form>

{#if submissionStatus === 'success'}
  <div>
    <h3>Form Submitted Successfully!</h3>
    <p>First Name: {submissionData.firstName}</p>
    <p>Surname: {submissionData.surname}</p>
    <p>Email: {submissionData.email}</p>
    <p>Password: {submissionData.password}</p>
    <p>Mobile: {submissionData.mobile}</p>
  </div>
{/if}

<style>
  @import 'bootstrap/dist/css/bootstrap.min.css';
</style>

