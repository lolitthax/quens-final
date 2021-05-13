<template>
  <div>
    <div class="q-gutter-y-md" style="max-width: 100%">
  

      <q-tabs
        v-model="tab"
        inline-label
        mobile-arrows
        class="bg-pink-5 text-white shadow-2"
      >
        <q-tab name="mails" icon="library_books" label="Sobre" />
        <q-tab name="alarms" icon="favorite" label="Personagens" />
        <q-tab name="movies" icon="school" label="Departamentos" />
          <q-tab name="movies" icon="home" label="Voltar a Dashboard" />

      </q-tabs>


    </div>
      <div class="q-pa-md" style="max-width: 100%; margin-top:10px;">
        <q-input outlined v-model="codigo" label="Código" style="margin-bottom: 10px"/>   
         <q-input outlined v-model="titulo" label="Título" style="margin-bottom: 10px"/>  
    <q-input
      v-model="descricao"
      filled
      type="textarea"
      label="Texto"
      style="margin-bottom: 15px"
    />
        <q-btn color="secondary" class="full-width" label="Salvar" @click="adicionarSobre()" />

  </div>
    <div class="q-pa-md" style="max-width: 100%">
    <q-list bordered>
      <q-item clickable v-ripple v-for="(sobre, index) in listaSobre" :key="index">
        <q-item-section avatar>
          <q-icon color="primary" name="bluetooth" />
        </q-item-section>
        <q-item-section> {{ sobre.codigo }} - {{ sobre.titulo }} - {{ sobre.descricao }} </q-item-section>
        <q-item-section top side>
          <div class="text-grey-8 q-gutter-xs">
            <q-btn class="gt-xs" size="12px" flat dense round icon="delete" @click="removerSobre(index)" />
            <q-btn class="gt-xs" size="12px" flat dense round icon="visibility" />
    
          </div>
        </q-item-section>
      </q-item>
      </q-list>
      </div>
  </div>
  
</template>
<script>
export default{
    data(){
        return{
            codigo: '',
            titulo: '',
            descricao: '',
            listaSobre: [
                {codigo:1, titulo: 'Texto', descricao: 'Texto'},
                {codigo:2, titulo: 'Texto', descricao: 'Texto'}
            ]
        }
    },
    methods: {
        adicionarSobre(){
            this.listaSobre.push( {codigo: this.codigo, titulo:
            this.titulo, descricao: this.descricao} )
        this.codigo = ''
        this.titulo = ''
        this.descricao = ''
        },
        removerSobre(index){
            this.$q.dialog({
                title: 'Excluir',
                message: 'Deseja excluir este item?',
                cancel: {
                    label: 'Cancelar'
                },
                ok: {
                    label: 'Excluir'
                },
                persistent: true
            }).onOk(() => {
                this.listaSobre.splice(index,1)
                    this.$q.notify({
                        message: 'Item removido!',
                        icon: 'done',
                        color: 'positive'
                    })
            }).onCancel(() => {

            })
            
        }
    }
}
</script>

