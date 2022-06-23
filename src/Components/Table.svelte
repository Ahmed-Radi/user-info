<script>
    export let data;
    export let handleDelete;
    export let handleEdit;
</script>
{#await data}
    <p>waiting...</p>
{:then data}
    {#if Object.keys(data).length !== 0}
    <section class="table-container">
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th colspan="2">Action</th>
                </tr>
            </thead>
            <tbody>
                {#each data as person (person.id)}
                    <tr>
                        <td>{person.name}</td>
                        <td><a href={`mailto:${person.email}`}>{person.email}</a></td>
                        <td><button class="action-button" on:click={() => handleEdit(person.id)}>Edit</button></td>
                        <td><button class="action-button" on:click={() => handleDelete(person.id)}>Remove</button></td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </section>
    {:else}
        <div class="empty-data">
            <p>No pepole ...</p>
        </div>
    {/if}
{/await}

<style>
    th {
        border-bottom: 1px solid;
    }
    td {
        padding: 5px;
    }
    td:nth-child(1),
    td:nth-child(1) {
        max-width: 300px;
    }
    table {
        margin: 10px auto;
        word-wrap: break-word;
        /* border-collapse: collapse; */
    }
    tr > th {
        background-color: #fff;
    }
    tr:hover {
        background-color: #52c0ff28;
    }
    .empty-data {
        color: red;
        text-align: center;
    }
    @media (min-width: 0px) and (max-width: 555px) {
        .table-container {
            overflow-x: scroll;
        }
        td:nth-child(1),td:nth-child(2) { min-width: 150px; }
    }

    /* tr:nth-child(odd) {
        background-color: #00ECFF;
    } */
    /* tr:nth-child(odd):hover {
        background-color: rgba(0, 238, 255, 0.675);
    }
    tr:nth-child(even) {
        background-color: #00D2FF;
    }
    tr:nth-child(even):hover {
        background-color: rgba(0, 208, 255, 0.4);
    } */
</style>
