<template>
    <!-- Componente responsável por exibir as informações detalhadas do bot -->
    <div class="details">        
        <div class="header">   
            <div class="bot-id">
                id: {{ filter = $route.params.id}}
            </div>
            <my-image class="bot-img" :src="filteredBot[0].image" :alt="filteredBot[0].description"/>        
            <p class="bot-name">{{filteredBot[0].name}}</p>          
            <p class="bot-date">Created at {{ filteredBot[0].created.substr(0, 10).split('-').reverse().join('/') }}</p>   
            <div class="clear-both"></div>
        </div>
        <div class="line"></div>
        <div class="row">        
            <div class="box-local col-xl-3">
                <p>Region and idiom</p>
                <p class="bold">{{filteredBot[0].culture}}</p>
                <p>Timezone</p>
                <p class="bold">(UTC - 03:00) Brasília</p>
            </div>            
            <div class="box-actived-user col-xl-6">
                <div class="box-img">
                    <my-image  :src="imageUserSrc" :alt="imageUserAlt"/> 
                </div>
                <div class="box-text">
                    <p class="title">{{filteredBot[0].analytics.user.actived}}</p>
                    <p class="subtitle">Usuários ativos</p>
                </div>
            </div>
            <div class="box-msg-receveid col-xl-6">
                <div class="box-img">
                    <my-image  :src="imageReceivedSrc" :alt="imageReceivedAlt"/> 
                </div>
                <div class="box-text">
                    <p class="title">{{filteredBot[0].analytics.message.received}}</p>
                    <p class="subtitle">Mensagens recebidas</p>
                </div>   
            </div>
            <div class="box-msg-sent col-xl-3">
                <div class="box-img">
                    <my-image  :src="imageSentSrc" :alt="imageSentAlt"/>
                </div>
                <div class="box-text">
                    <p class="title">{{filteredBot[0].analytics.message.sent}}</p>
                    <p class="subtitle">Mensagens recebidas</p>
                </div>
            </div>
            <div class="box-status-account col-xl-3">
                <my-image  :src="imageStatusAccSrc" :alt="imageStatusAccAlt"/> 
                <p class="subtitle">Status Account</p>
                <p class="title">Free</p>
                <my-button :title="buttonUpdate" :type="'text'"  :class="'btn'" />                
            </div>             
        </div>       
        <div class="line"></div>                             
    </div>

</template>

<script>

import json from '../../../assets/resources/data.json';
import Image from '../../shared/image/Image';
import Button from '../../shared/button/Button';


export default{ 
    components:{
        'my-image': Image,
        'my-button': Button
    },
    data(){
        return{
            bots: json,
            filter: '',
            imageUserSrc: require('../../../assets/images/user.png'),
            imageUserAlt: 'Usuários ativos',
            imageReceivedSrc: require('../../../assets/images/sent.png'),
            imageReceivedAlt: 'Usuários ativos',
            imageSentSrc: require('../../../assets/images/sent.png'),
            imageSentAlt: 'Usuários ativos',                        
            imageStatusAccSrc: require('../../../assets/images/plano.png'),
            imageStatusAccAlt: 'Usuários ativos',
            buttonType: 'submit',
            buttonStyle: 'btn',
            buttonUpdate: 'Update account'
        }
    },
    computed:{
        // Método que retorna qual bot foi clicado
        filteredBot(){
            if(this.filter){
                let exp = new RegExp(this.filter.trim(), 'i');
                return this.bots.filter(bot => exp.test(bot.shortName));
            }else{
                return [];
            }
        },
    },


}
</script>

<style lang="scss" src="./style.scss" scoped >

</style>