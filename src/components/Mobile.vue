<template>
    <div v-if="numResults === 0" class="mobileBackground">
        <b-img 
        src="/logo.png"
        contain
        >
        </b-img>
    </div>
    <div v-else class="text-left resSection">
        <div class="labelBar">
        <span class="fromText">From 
            <b-img
            src="icon_arrow01.svg"
            class="iconImage"
            >
            </b-img></span>
            <span class="labels"> | <b>To</b> | <b>Subject</b> | <b>Date</b></span>
        </div>
        <div v-for="result in results" v-bind:key="result.from" class="resItems" @click="result.active = !result.active">
            <span>
                <b-img
                src="icon_mail_sp.svg"
                contain
                class="inboxImage"
                >
                </b-img>
                <span class="fromData">{{result.from}}
                </span>
                <span class="timeData">{{result.formatDate}}
                <span v-if="result.attachments===true">
                    <b-img 
                        src="icon_clip.svg"
                        contain
                        class="attachImage"
                        >
                    </b-img>
                </span>
                <b-img
                src="icon_arrow02.svg"
                contain
                class="arrowImage"
                >
                </b-img>
                </span>
            </span>
            <div v-if="result.to.lenght < 2"><span> {{result.to[0]}}</span></div>
            <div v-if="result.to.length < 3"><span>  {{result.to[0]}}, {{result.to[1]}}</span></div>
            <div v-else><span>{{result.to[0]}}, {{result.to[1]}}, ... <b-badge class="toBadge"> +{{result.to.length -2 }} </b-badge></span></div>
            <div class="subjectText">{{result.subject}}</div>
            <div v-if="result.active">
                <b-card no-body class="card bg-light">
                    <b-card-text class="cardText"> {{result.body}} </b-card-text>
                </b-card>
            </div>
        </div>
    
    </div>

</template>

<script>
export default {
    props: ["results", "numResults","fields", "sortBy", "sortDesc"],
    
}
</script>

<style scoped>
.mobileBackground{
    border-top: 2px solid;
    border-color: lightgrey;
    padding-top: 50%;
    margin-left : -20px;
    padding-left : 20px

}
.iconImage{
    height : 12px;
    width : 12px;
}
.fromText{
    font-size: 13px;
    font-weight: bold;
    padding-left: 10px;
}
.labels{
    font-size: 13px;
    color: rgb(95, 95, 95);
    word-spacing: 5px;   
}

.labelBar{
   background-color: #e9e9e9;
    margin-left : -20px;
    padding: 10px;
    border-top : 1px solid;
    border-bottom :1px solid;
    border-color: #d3d3d3;

}
.inboxImage{
    height: 25px;
    width : 25px;
    float :left;
    margin-left: -5px;
    margin-top:5px;
    vertical-align: middle;
}
.tablehead{
  background-color:#e9e9e9 !important;
  color: rgb(95, 95, 95);
}
/* .resSection{
    padding-top: 10px;
    padding-bottom: 20px;
    margin-left : -20px;
    float: left;
    background-color: #e9e9e9 ;
} */
.resSection{
    font-size: 12px;
}
.resItems{
    padding-left :15px;
    padding-right:25px;

    padding-top:10px;
    padding-bottom:10px ;
    border-bottom: 1px solid;
    margin-left: -20px;
    border-color: lightgrey;
    background-color: white;
}
.fromData{
     font-weight: bold;
     vertical-align:top;
     position: relative;
     top:-1px;
}
.timeData{
    float: right;
    vertical-align:middle;
}
.arrowImage{
    height:5px;
    width:5px;
    float:right;
    position:absolute;
    right:15px;
    margin-top: 6px;
}
.subjectText{
    font-size: 14px;
}
.attachImage{
    height:12px;
    width:12px;
    float:left;
    position: relative;
    margin-top: 2px;
    margin-right: 5px ;
}
.card{
    font-size:10pt !important;
    padding:2px !important
}
.cardText{
    padding : 2px !important
}
</style>
