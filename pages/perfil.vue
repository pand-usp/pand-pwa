<template>
    <v-container>
        <div v-if="showUser" class="secondary rounded-circle bold" style="width:32px;height:32px;justify-content:center;display:flex;"> 
            <p class="mt-8 font-weight-bold" style="align-self:center;">F</p> 
        </div>
        <v-card-actions class="d-flex flex-column" align-items="center" width="auto">
            <v-btn
                class="text-xs-center black--text" 
                color="primary"
                elevation="2"
            >
                Cadastrar local
            </v-btn>
        </v-card-actions>
    </v-container>
</template>

<script>

</script>
