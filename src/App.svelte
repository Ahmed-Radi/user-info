<script>
    import Form from "./Components/Form.svelte";
    import Modal from "./Components/Modal.svelte";
    import Table from "./Components/Table.svelte";
    import EditForm from './Components/EditForm.svelte';
    let isOpen = false;
    let editPerson;
    let data;
    async function fetchUsers() {
		const response = await self.fetch('https://jsonplaceholder.typicode.com/users');
		if (response.ok) {
            return response.json();
		} else {
			throw new Error(users);
		}
	}
    // asign data into data variable
    data = fetchUsers()
    // convert API data from Promise to data
    Promise.all([data]).then((values) => {
        data = values[0];
    });

    const handleDelete = (id) => {
        data = data.filter(person => person.id !== id)
    }
    const handleEdit = (id) => {
        editPerson = data.filter(person => person.id === id)
        isOpen = true
    }
    const handleSetEdit = (e) => {
        // target user to changes his data
        let newdata = data.filter(p => p.id === e.detail.id)
        //change name and email
        newdata[0].name = e.detail.name
        newdata[0].email = e.detail.email
        // change legacy data with new data
        data = data
    }
    const modalToggle = () => {
        isOpen = !isOpen;
    }

    /***/
    const addPerson = (e) => {
        data = [e.detail, ...data]
    }
</script>

<Modal isOpen={isOpen} modalToggle={modalToggle}>
    <div slot="title">
        <p>update user info</p>
    </div>
    <EditForm editPerson={editPerson} on:editPerson={handleSetEdit} />
</Modal>
<main>
	<h1 class="header">User Info</h1>
    <Form on:addPerson={addPerson} />
    <Table data={data} {handleDelete} {handleEdit} />
</main>

<style>
    .header {
        text-align: center;
    }
</style>