<template>
  <div>
    <base-header class="header pb-2 pt-3 pt-lg-6 d-flex align-items-center">
      <!--style="min-height: 600px; background-image: url(img/theme/profile-cover.jpg); background-size: cover; background-position: center top;">-->
      <!-- Mask -->
      <span class="mask bg-gradient-success opacity-8"></span>
      <!-- Header container -->
    </base-header>

    <div class="container-fluid">
      <br>
        <b-tabs content-class="mt-3" justified>
          <b-tab title="Maitre D'Ouvrage" active>
            <b-table ref="selectableTable" :items="items" :fields="fields">
              <template v-slot:cell(id)="{item}">
                ++{{ item.id }}
              </template>
              <template v-slot:cell(action)="row">
                <b-button variant="outline-warning" size="sm" @click="info(row.item, $event.target)" class="mr-1">
                  Modifier
                </b-button>
                <b-button variant="outline-danger" size="sm" class="mr-1" v-b-modal.suppressionParticipant>
                  Supprimer
                </b-button>
              </template>

            </b-table>
          </b-tab>
          <b-tab title="Entreprise">
            <b-table ref="selectableTable" :items="items" :fields="fields">
              <template v-slot:cell(id)="{item}">
                ++{{ item.id }}
              </template>
              <template v-slot:cell(action)="row">
                <b-button variant="outline-warning" size="sm" @click="info(row.item, $event.target)" class="mr-1">
                  Modifier
                </b-button>
                <b-button variant="outline-danger" size="sm" class="mr-1" v-b-modal.suppressionParticipant>
                  Supprimer
                </b-button>
              </template>

            </b-table>
          </b-tab>
          <b-tab title="Mairie">
            <b-table ref="selectableTable" :items="items2" :fields="fields">
              <template v-slot:cell(id)="{item}">
                ++{{ item.id }}
              </template>
              <template v-slot:cell(action)="row">
                <b-button variant="outline-warning" size="sm" @click="info(row.item, $event.target)" class="mr-1">
                  Modifier
                </b-button>
                <b-button variant="outline-danger" size="sm" class="mr-1" v-b-modal.suppressionParticipant>
                  Supprimer
                </b-button>
              </template>

            </b-table>
          </b-tab>
          <b-tab title="Bureau Etude"><p>I'm a disabled tab!</p></b-tab>
          <b-tab title="Promoteur"><p>I'm a disabled tab!</p></b-tab>
        </b-tabs>
        <b-button v-b-modal.modal-1 variant="primary">Ajouter un Participant</b-button>
    </div>
    <b-modal id="suppressionParticipant" title="Supprimer Un Participant" ok-variant="false">
      <p class="my-4">Etes-vous sûr de supprimer le participant sélectionné ?</p>
      <template v-slot:modal-footer="{ close, ok }">
        <!-- Emulate built in modal footer ok and cancel button actions -->
        <b-button size="sm" variant="success" @click="close()">
          Annuler
        </b-button>
        <b-button size="sm" variant="danger" @click="ok()">
          Supprimer
        </b-button>
      </template>
    </b-modal>
    <b-modal id="modal-1" title="Selectionner votre Type de Participant">
      <b-button v-b-modal.modal-MO variant="outline-primary">Maitre D'Ouvrage</b-button>
      <br>
      <b-button v-b-modal.modal-P variant="outline-primary">Promoteur</b-button>
      <br>
      <b-button v-b-modal.modal-M variant="outline-primary">Mairie</b-button>
      <br>
      <b-button v-b-modal.modal-E variant="outline-primary">Entreprise</b-button>
      <br>
      <b-button v-b-modal.modal-BE variant="outline-primary">Bureau Etude</b-button>
    </b-modal>
    <b-modal id="modal-MO" size="lg" title="Ajout Maitre D'Ouvrage">
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
            label-cols-sm="3"
            label="Street:"
            label-align-sm="right"
            label-for="nested-street"
        >
          <b-form-input id="nested-street"></b-form-input>
        </b-form-group>

        <b-form-group
            label-cols-sm="3"
            label="City:"
            label-align-sm="right"
            label-for="nested-city"
        >
          <b-form-input id="nested-city"></b-form-input>
        </b-form-group>

        <b-form-group
            label-cols-sm="3"
            label="State:"
            label-align-sm="right"
            label-for="nested-state"
        >
          <b-form-input id="nested-state"></b-form-input>
        </b-form-group>

        <b-form-group
            label-cols-sm="3"
            label="Country:"
            label-align-sm="right"
            label-for="nested-country"
        >
          <b-form-input id="nested-country"></b-form-input>
        </b-form-group>

        <b-form-group
            label-cols-sm="3"
            label="Ship via:"
            label-align-sm="right" class="mb-0"
        >
          <b-form-radio-group
              class="pt-2"
              :options="['Air', 'Courier', 'Mail']"
          ></b-form-radio-group>
        </b-form-group>
      </form>
    </b-modal>
    <b-modal id="modal-P" size="lg" title="Ajout Promoteur"></b-modal>
    <b-modal id="modal-M" size="lg" title="Ajout Mairie"></b-modal>
    <b-modal id="modal-E" size="lg" title="Ajout Entreprise"></b-modal>
    <b-modal id="modal-BE" size="lg" title="Bureau Etude"></b-modal>

  </div>
</template>
<script>
export default {
  name: 'user-profile',
  data() {
    return {
      fields: [{key:'nom' , label:'Nom'}, {key:'prenom' , label:'Société' }, {key:'contact' , label:'email' }, {key:'tata' , label:'Droit Accès' }, {key:'tonton' , label:'Enregistrer' },{key:'action', label: ''}],

      items:[
         {nom: 'Snow', prenom: 'Jon', contact: '@youknownothing'},
        {nom: 'Skylwalker', prenom: 'Luke', contact: '@usetheforce'},
        {nom: 'Lodbrok', prenom: 'Ragnar', contact: '@odinforever'},
        {nom: 'Moi'},
  ],
      items2:[
        {nom: 'Snow', prenom: 'Jon', contact: '@youknownothing'},
        {nom: 'Skylwalker', prenom: 'Luke', contact: '@usetheforce'},
      ],
    }
  },
};
</script>
<style></style>
