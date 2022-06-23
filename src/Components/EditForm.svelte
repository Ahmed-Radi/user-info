<script>
    import { createEventDispatcher } from 'svelte';
    export let editPerson;
    let dispatch = createEventDispatcher()
    let error = false;
    let email;
    const handleEditSubmit = () => {
        if ( editPerson[0].name &&  editPerson[0].email) {
            let newEditPerson = {
                name: editPerson[0].name,
                email: editPerson[0].email,
                id: editPerson[0].id
            }
            dispatch('editPerson', newEditPerson)
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
    <form on:submit|preventDefault={handleEditSubmit}>
        <label for="name">
            <span class="form_label">Name:</span>
            <input type="text" id="name" placeholder="Enter your name" class="form__input" bind:value={editPerson[0].name} />
        </label>
        <label for="email">
            <span class="form_label">Email:</span>
            <input type="text" id="email" placeholder="Enter your email" class="form__input" bind:value={editPerson[0].email} />
        </label>
        <button class="action-button">Update</button>
    </form>
</section>
<style>
    .error {
        color: red;
        transition: all 0.5s ease-in;
    }
    .form_label {
        display: inline-block;
        width: 60px;
    }
</style>