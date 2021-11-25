<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMOde">Add Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
    import AddResource from './AddResource'
    import StoredResources from './StoredResorces'
    export default {
        components: {
            AddResource,
            StoredResources
        },
        computed: {
            storedResButtonMode() {
                return this.selectedTab === 'stored-resources' ? null : 'flat';
            },
            addResButtonMOde() {
                return this.selectedTab === 'add-resource' ? null : 'flat';
            }
        },
        data() {
            return {
                selectedTab: 'stored-resources',
                storedResources: [
                    {
                        id: 'youtube',
                        title: 'Youtube',
                        description: 'You can learn anything from YouTube!',
                        link: 'https://vuejs.org'
                    },
                    {
                        id: 'google',
                        title: 'Google',
                        description: 'Google is the best!',
                        link: 'https://google.com'
                    },
                    {
                        id: 'mdn',
                        title: 'MDN Web Docs',
                        description: 'My go-to resource for JavaScript documentation.',
                        link: 'https://vuejs.org'
                    }
                ]
            }
        },
        methods: {
            setSelectedTab(tab) {
                this.selectedTab = tab;
            },
            getNewResource(title, description, link) {
                const newResource = {
                    id: new Date().toISOString(),
                    title: title,
                    description: description,
                    link: link
                };
                this.storedResources.unshift(newResource);
                this.selectedTab = 'storedResources'
            },
            deleteResource(id) {
                const resIndex = this.storedResources.findIndex(res => res.id === id);
                this.storedResources.splice(resIndex, 1);
            }
        },
        provide() {
            return {
                resources: this.storedResources,
                addResource: this.getNewResource,
                deleteResource: this.deleteResource
            }
        }
    }
</script>

<style></style>