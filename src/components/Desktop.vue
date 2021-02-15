<template>
    
<div v-if="numResults === 0" class="background">
    <b-img 
    src="/logo.png"
    contain
    >
    </b-img>
  </div>
    <div v-else class="resultTable text-left">
      <b-table 
      :items="results" 
      :fields="fields" 
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      thead-class="thead"
      tbody-tr-class="rowClass"
      @row-clicked="OnRowClicked"
      >
        <template #cell(from)='data' >
          <span v-if="data.item.from.length > 15">
            {{data.item.from.substring(0,15)}}...
          </span>
          <span v-else>
            {{data.item.from}}
          </span>
        </template>
          
        <template #cell(to)='data'>
          {{data.item.to[0]}}<span v-if="data.item.to.length > 1">, ...<b-badge class="toBadge"> +{{data.item.to.length -1 }} </b-badge></span>
        </template>

        <template #cell(subject)='data'>
          {{data.item.subject}} 
          <span v-if="data.item.attachments === true"> 
            <b-img 
            src="icon_clip.svg"
            contain
            class="subAttach"
            >
            </b-img>
          </span>
        </template>

        <template #head(formatDate)="data">
          <span class ="dateText">
          {{data.label}}
            <b-img
            src="icon_arrow01.svg"
            contain
            height="15"
            width="15"
            >
            </b-img>
          </span>
        </template>
        <template #row-details="row">
            <b-card class="card bg-light mb-3" :title="row.item.subject" :sub-title="row.item.formatDate">
                <b-card-text>
                <div><b> From: </b> {{row.item.from}}</div>
                <div><b> To: </b><span v-for="(tos,index) in row.item.to" :key="tos">{{tos}}<span v-if="index < row.item.to.length-1">, </span> </span></div>
                <div class="cardBody">{{row.item.body}}</div>
                </b-card-text>
                <div v-if="row.item.attachments">
                    <b-button title="Download Attachments"><b-icon icon="cloud-download" aria-hidden="true"></b-icon> Download Attachments
                    </b-button>
                </div>
            </b-card>
        </template>
      </b-table>
    </div>
</template>

<script>
export default {
    props: ["results", "numResults","fields", "sortBy", "sortDesc"],

    methods:{
        OnRowClicked(item){
            item._showDetails = !item._showDetails
            console.log(item._showDetails)
        }

    }
}
</script>

<style >
.cardBody{
    padding-top : 5px;
}
.card{
    color:black;
}

.col-md-7{
  padding-bottom: 10px  !important;
  padding-left :0px;
}
.background{
  border-top: 2px solid;
  border-color: lightgrey;
  padding-top: 20%;
  padding-bottom: 20%;
  margin-left: 15px;
  margin-right: 15px;
}
.fromCol{
  max-width : 110px;
}
.rowClass{
  font-size: 18px;
}
.rowClass:hover{
  color : blue;
  cursor: pointer;
}
.rowClass:hover .subAttach{
  filter: invert(9%) sepia(99%) saturate(6598%) hue-rotate(248deg) brightness(100%) contrast(147%);
}

.toCol{
  max-width : 200px;
  padding-right: 30px !important;
}
.subjectCol{
  max-width : 50%;
  padding-right : 0px !important;
}
.toBadge{
  float : right;
  background-color:#A9A9A9 !important;
}
.subAttach{
  float : right;
  margin-top: 5px;
  height: 20px;
  width:20px;
}
.tableRow:hover{
  color : blue !important;
}
.resultTable{
  padding-left : 15px;
}
.thead{
  background-color:#e9e9e9;
  color: rgb(95, 95, 95);
}
.dateText{
  font-weight:bold;
  color : black
}

</style>