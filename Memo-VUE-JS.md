# Vue.js 

Ressources : 
* Github Librairies, bonnes pratiques : [Lien Github](https://github.com/vuejs/awesome-vue)

## Mémo Cordova + Vue.js 

| Répertoire | Contenu
| :-------:| ---------|
| build | 
| config |
| node_modules |
| resources |
| src |
| static |
| www | 


| Commande | Utilisation 
| :-------:| ---------|
| npm run dev | 
| npm run build | 


## Utilisation Vue.js 

### Charger la librairie Vue.js avec un CDN & Vue DevTools

Ajouter dans les liens (comme par exemple : Bootstrap, jQuery..), la liaison avec la librairie Vue.js :
```
<script src="https://cdn.jsdelivr.net/npm/vue"></script> // Vue.js
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.13/dist/vue.js"></script> //Vue DevTools
```

#### Récupérer un texte entré dans un champ saisie 

```
<div id="app">
    <label for="titre">Titre : </label>
    <input type="text" id="titre" v-model="titre"/>
    <h1>{{titre }}</h1>
</div>

<script>
    var app = new Vue({
        el : '#app',
        data :{
            titre : ''
        }
    })
</script>
```


#### Récupérer un texte entré lors d'un évènement 

Lorsque je clique sur un bouton, le titre prend la valeur de mon input

```
<div id="app">
    <label for="titreh2" autofocus>Mon petit titre : </label>
    <input type="text" id="titreh2" v-model="titreh2"/>
    <button v-on:click="affiche">Ajouter un titre</button>  // alternative : v-on:click="titreAffiche = titreh2"
    <h2>{{titreAffiche }}</h2>
</div>

<script>
    var app = new Vue({
        el: '#app',
        data: {
            titreh2: '',
            titreAffiche: ''
        },
        methods: {
            affiche: function () {
                this.titreAffiche = this.titreh2 
            }
        }
    })

</script>
```


#### Changer des classes 

Lorsque je coche ma checkbox, les titres sont en rouge (class "red" dans style.css mettant en rouge)

```
<h2 :class="{red : isRed}">{{titreAffiche }}</h2> // la classe "red" est appliquée si "isRed" est "true"
// :class et v-bind:class sont 2 syntaxes identiques

<input type="checkbox" v-model="isRed">Je vois Rouge</input> // v-model me permet de récupérer la valeur de mon input
```

#### Apparaître - disparaître 

2 possibilités pour afficher ou cacher un élément : 
* v-if : lorsque l'élément n'est pas affiché, il n'est pas présent dans le code 
* v-show : à l'inverse, même lorsqu'il est caché l'élément est présent dans le code

```html
<input type="checkbox" v-model="show">Magie Magie !</input>

<img v-if="show" id="crashounet" src="crash.png"/> // Si show = true alors l'image s'affiche
<img v-show="show" id="crashounet" src="crash.png"/> 
```


#### Boucle v-for
boucle : rajouter des clés

[documentation officielle](https://fr.vuejs.org/v2/guide/list.html)


```javascript
<template>
    <div>
        <h1>Liste des machines</h1>
        <machine v-for="machine in machines" :key="machine.id" :name="machine.name" :status="machine.status" :checked-at="machine.checkedAt"></machine>
    </div>
</template>

<script>
    import Machine from './Machine.vue';

    export default {
        components: {Machine},
        name: "machine-list",
        data() {
            return {
                machines: [{
                    id: 1,
                    name: 'What else ?',
                    status: true,
                    checkedAt: new Date(),
                }, {
                    id: 2,
                    name: 'Broken',
                    status: false,
                    checkedAt: new Date(),
                }]
            }
        }
    }
</script>
```

**Important : key**
Une boucle v-for demande la présence d'une clé (id), il faut donc préciser lorsqu'on fait la boucle qu'il existe un 'id' servant de 'key'
```javasript
<machine v-for="machine in machines" :key="machine.id">
```



## Mettre en place un projet buildé avec "vue-cli"

* Installer Vue-cli 
```bash
# install vue-cli
    $ npm install --global vue-cli
# create a new project using the "webpack" template
    $ vue init webpack-simple NomDuProjet
# install dependencies and go!
    $ cd my-project
    $ npm install
    $ npm run dev
```

* Webpack-simple : est un template de Vue.js

* Réponses aux questions lors du "vue init webpack"
    * nom du projet
    * description
    * auteur 
    * Licence MIT : appuyer sur entrée ou renseigner MIT
    * Use sass ? yes 

### Webpack 

Webpack permet de morceler le code sous forme de modules qui seront ensuite fusionnés en un seul fichier par Webpack.


## Ajouter un composant externe avec NPM : toggle button 

Ressources : [Lien Github](https://github.com/euvl/vue-js-toggle-button)

* Installer le composant en ligne de commande dans le projet 
```bash
npm install vue-js-toggle-button --save
```

* Importer dans le fichier "main.js" le composant 
```javascript
import ToggleButton from 'vue-js-toggle-button'
Vue.use(ToggleButton)
```

* Dans le html 
```html 
<toggle-button @change="onChangeEventHandler"/>

<toggle-button v-model="myDataVariable"/>

<toggle-button :value="false" 
               color="#82C7EB" 
               :sync="true" 
               :labels="true"/>

<toggle-button :value="true" 
               :labels="{checked: 'Foo', unchecked: 'Bar'}"/>
``` 

## Créer un composant 

Un composant est un élément personnalisable. Un peu comme une fonction pour du HTML.

Le composant est composé de :
* 'props' : données 
* 'template' : html 


**Exemple : composant 'test' affichant un titre H2**

* Créer le composant dans le fichier "main.js"
```javascript
Vue.component('test', {
  props: ['message'],
  template : `<h2>{{message}}</h2>`
});
```


```javascript
Vue.component('test', {
  props: ['message'],
  template : `<h2>{{message}}</h2>`
});

Vue.component('machine', {
  props: ['nom', 'active'],
  template : `<li :class="{red : !active}">{{nom}}<toggle-button :labels="{checked: 'on', unchecked:'off'}" v-model="active"/></li>`
});
```

```html
<test message="Liste des machines"></test>

<ul>
   <machine v-bind:nom="machine.name" v-bind:active="machine.status" v-for="machine in machines"></machine>
</ul>
```


## Créer un composant dans un autre fichier

En Vue.js tout est composant, pour faire un nouvel écran il nous faut un nouveau composant. 

Avec WebStorm : 
* Créer un nouveau fichier dans "src" en allant sur "File/New/Vue Component"
* Donner un nom de fichier "monfichier" sans l'extension ".vue"

Le composant "MachineList.vue" a la structure suivante :
```javascript
<template> // Mettre les élément dans une <div>
    <div>
        <h1>Mon titre</h1>
    </div>
</template>

<script>
    export default {
        name: "machine-list" //nom de la balise qui permettra d'appeler le composant
    }
</script>

<style scoped>
    div{
        background-color: aqua; //scoped permet d'appliquer le style uniquement au composant sans impacter le reste
    }

</style>
```

Dans le fichier "app.vue" afficher le composant :
* afficher le composant dans la div "app"
```javascript
<template>
    <div id="app">
        <machine-list></machine-list> //le composant est affiché
    </div>
</template>
```
* Importer le composant dans le script 
```javascript
<script>
    import MachineList from "./MachineList.vue"; //importer le composant 
```
* Déclarer le compsant 
```javascript
export default {
        components: {MachineList}, //déclarer le composant 
}
```

*A noter, dans WebStorm, il suffit simplement d'afficher le composant avec les balises et les importations et déclarations se font automatiquement **mais il faut ajouter '.vue' dans l'importation du composant***

* Vue globale du fichier 'app.vue'
```javascript
<template>
    <div id="app">
        <machine-list></machine-list> //le composant est affiché
    </div>
</template>

<script>
    import MachineList from "./MachineList.vue"; //importer le composant 

    export default {
        components: {MachineList, Machine}, //déclarer le composant 
        name: 'app',
        data() {
            return {
                msg: 'Welcome to Your Vue.js App',
            }
        },
        methods: {
            onMachinesListClick : function(){
                alert("consulter la liste des machines"); //afficher un message lorsqu'on click sur le bouton "liste machines"
            },
            onMapClick : function(){
                alert("consulter la carte"); //afficher un message lorsqu'on click sur le bouton "carte"
            }
        }
    }
</script>
```

### Passer des données : props

**Exemple**

Fichier du composant "Machine.vue" :

```
<template>
    <div>
        <h1>{{name}}</h1>
        <h3 v-if="status" class="green">Status {{msgMachineOk}}</h3>
        <h3 v-if="!status" class="red">Status {{msgMachineKo}}</h3>
        <h5>Dernière vérification : {{formatDate(checkedAt)}}</h5>
    </div>

</template>

<script>
    export default {
        name: "machine",
        props: ['name', 'status', "checkedAt"], //Je déclare mes props
        data() {
            return {
                msgMachineKo : 'KO',
                msgMachineOk : "OK",
            }
        },
        methods: {
            formatDate : function(dateBrute){
                return dateBrute.toLocaleString('fr-FR', {timeZone: 'UTC'});
            }
        }
    }
</script>
```

* Les props sont déclarées dans 'export default'
* Je place dans mon template les props 
```javascript
<h1>{{name}}</h1>
<h3 v-if="status"></h3>
``` 


Utilisation du composant dans un autre composant "MachineList.vue":

```
<template>
    <div>
        <h1>Liste des machines</h1>
        <!--<machine name="mamachine" status="true" checkedAt="12/03/2018"></machine>-->
        <machine :name="machine.name" :status="machine.status" :checked-at="machine.checkedAt"></machine>
    </div>
</template>

<script>
    import Machine from './Machine.vue';

    export default {
        components: {Machine},
        name: "machine-list",
        data() {
            return {
                machine: {
                    id: 1,
                    name: 'What else ?',
                    status: true,
                    checkedAt: new Date(),
                }
            }
        }
    }
</script>
```

* Pour passer des données dans un attribut, il faut ajouter ':' devant l'attribut : ':name="machine.name' (idem que v-bind:name="machine.name")



# Mise en place d'un routeur

Le problème est que nous ne voulons pas avoir une seule page sur notre application. Nous devons avoir la possibilité de naviguer d'une page à l'autre, sans recharger la page ou sans afficher une nouvelle page html, nous avons besoin de mettre en place un routeur.

C'est la même chose que Laravel, sauf qu'ici le routeur est côté client, nous devons définir nos routes côté client et avoir moyen d'en changer.

Cela tombe bien, Vue a un routeur tout prêt que nous allons utiliser, [vue-router](https://router.vuejs.org/fr/installation.html)

## Installation 

#### Installation avec NPM

* Avec npm, lancer la commande :
```bash
npm install vue-router
```

* Dans le fichier "main.js", importer VueRouter 
```javascript
import VueRouter from 'vue-router'
Vue.use(VueRouter) // a mettre avant (new Vue)
```

#### Téléchargement direct CDN

Unpkg.com fournit des liens CDN basés sur npm. Le lien ci-dessus pointera toujours vers la dernière version sur npm.
Incluez vue-router après Vue et l'installation sera automatique :

```javascript
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
```


## Utilisation du routeur 

Lien vers un exemple : [exemple](https://jsfiddle.net/yyx990803/xgrjzsup/)

#### Dans le fichier "main.js" : 

* Importer les composants 
```javascript
import MachineList from './MachineList.vue'
import MachinesMap from './MachinesMap.vue'
```
* Créer le tableau des routes 
```javascript
const routes = [
    {
        path: '/machines',
        component: MachineList
    },
    {
        path: '/map',
        component: MachinesMap
    },
]
```
* Créer une instance de route avec pour option "routes"
```javascript
const router = new VueRouter({
    routes
})
```
* Ajouter l'instance 'router' dans l'élément 'app' 
```javascript
new Vue({
    el: '#app',
    router, //ajouter l'instance router dans la Vue
    render: h => h(App)
})
```

#### Dans le fichier "app.vue"

* Appeler la route : balise 'router-link' et attribut 'to="/route"'
```javascript
<router-link to="/machines"  class="btn btn-lg btn-success">Consulter la liste des machines</router-link>
<router-link to="/map" class="btn btn-lg btn-success">Voir la carte</router-link>
```
* Ajouter la balise, une seule fois pour toutes les routes, en dessous des routes 
```javascript 
<router-view></router-view>
```


# Google Map


## Installer Google Map 

* Lancer la commande :
```
npm install vue2-google-maps
```

Documentation GitHub : [vue-google-maps](https://github.com/xkjyeah/vue-google-maps)

* Dans le fichier "main.js" :
```
import * as VueGoogleMaps from 'vue2-google-maps'
Vue.use(VueGoogleMaps, {
  load: {
    key: 'Notre_Cle_API', //à récupérer sur Google
  }
})
```

* Récupérer une clé API google Map : [En cliquant sur 'Obtenir une clé'](https://developers.google.com/maps/documentation/javascript/get-api-key?refresh=1)


## Afficher une Map

* Dans le template dans le fichier '.vue' :
```
<gmap-map
      class="maps"
      :center="{lat:45.1885, lng:5.7245}"
      :zoom="14"
    >
</gmap-map>
```

* Dans les balises 'style'
```
<style scoped>
.maps{
  width: 90%;
  height: 800px;
  margin: auto;
}
</style>
```

