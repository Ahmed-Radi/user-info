<script>
    export let isOpen = false;
    export let modalToggle;
    console.log(isOpen)

</script>
{#if isOpen}
    <section class="modal">
        <div class="modal__background" on:click|self={modalToggle}>
            <div class="modal__content">
                <slot name="title"></slot>
                <slot></slot>
            </div>
        </div>
    </section>
{/if}
<style>
    .modal__background {
        width: 100%;
        height: 100%;
        position: fixed;
        background-color: rgba(0, 0, 0, 0.8);
        margin-top: -19px;
    }
    .modal__content {
        padding: 20px;
        border-radius: 10px;
        max-width: 500px;
        margin: 10% auto;
        background: #fff;
    }
</style>