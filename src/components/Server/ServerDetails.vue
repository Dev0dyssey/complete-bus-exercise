<template>
    <div class="col-xs-12 col-sm-6">
        <p v-if="!server">Please select a Server</p>
        <p v-else>Server #{{ server.id }} selected, Status: {{ server.status }}, Role: {{ server.name }}</p>
        <hr>
        <button @click="resetStatus">Change to Normal</button>
        <button @click="assignRole">Change to Backup</button>
    </div>

</template>

<script>
    import { serverBus } from '../../main';

    export default {
        data: function() {
            return {
                server: null
            }
        },
        methods: {
          resetStatus() {
              this.server.status = 'Normal';
          },
          assignRole() {
              this.server.name = 'Backup';
          }
        },
        created() {
            serverBus.$on('serverSelected', (server) => {
                this.server = server;
            });
        }
    }
</script>

<style>

</style>
