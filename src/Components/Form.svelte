<script>
    import { createEventDispatcher } from 'svelte';
    let dispatch = createEventDispatcher()
    let name;
    let email;
    let error = false;
    const handleSubmit = () => {
        if (name && email) {
            dispatch('addPerson', {id: Math.random(), name, email})
            error = false
        } else {
            error = true
        }
    }
</script>

<section class="form">
    {#if error}
        <p class="error">Plase enter user name and email</p>
    {/if}
    <form on:submit|preventDefault={handleSubmit}>
        <label for="name">
            <span class="form_label">Name:</span>
            <input type="text" id="name" placeholder="Enter your name" class="form__input" bind:value={name} />
        </label>
        <label for="email">
            <span class="form_label">Email:</span>
            <input type="text" id="email" placeholder="Enter your email" class="form__input" bind:value={email} />
        </label>
        <button class="action-button">submit</button>
    </form>
</section>

<style>
    .error {
        color: red;
        transition: all 0.5s ease-in;
    }
    .form {
        width: 50%;
        margin: 50px auto;
    }
    .form_label {
        display: block;
        margin-bottom:  5px;
    }
    .form__input {
        width: 100%;
        border-radius: 5px;
    }
    @media (min-width: 0px) and (max-width: 480px) {
        .form {
            width: 100%;
        }
    }
</style>