<template>
    <base-dialog v-if="inputIsInvalid === true" title="Invalid Input" @close="inputIsInvalid = false">
        <template #default>
            <p>One of you're inputs is invalid</p>
            <p>Inputs can't be empty</p>
        </template>
        <template #actions>
            <base-button @click="inputIsInvalid = false">Ok</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" type="text" name="title" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea id="description" name="description" rows="3" ref="descriptionInput"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" type="url" name="link" ref="linkInput">
            </div>
            <base-button type="submit">Add Resource</base-button>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data() {
        return {
            inputIsInvalid: false
        }
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descriptionInput.value;
            const enteredLink = this.$refs.linkInput.value

            if (enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === '') {
                this.inputIsInvalid = true
                return
            }

            this.addResource(enteredTitle, enteredDescription, enteredLink);
        }
    }
}
</script>

<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>