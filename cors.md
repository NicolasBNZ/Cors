Questions

Quand je fais un fetch dans la console de la barre google, ça simule le fait que j'implémente une requete vers une api d'une autre origine? 

Dans la théorie, je suis sur le site de facebook, je tape l'adresse de l'api facebook, j'ai accès à tout!

Pourquoi une ip et un FQDN peuvent matcher? C’est grâce au DNS?




# Les cors

https://www.youtube.com/watch?v=4KHiSt0oLJ0
preflight = contrôle en amont
https://blog.webdevsimplified.com/2021-05/cors/
https://www.youtube.com/watch?v=h-WtIT6gCBk
https://www.youtube.com/watch?v=irpWV4effNE


    https://datahub-api.analytics.safran
fetch('https://datahub-api.analytics.safran').then(response=>response.json())
    https://api.datasquare.analytics.safran
fetch('https://api.datasquare.analytics.safran').then(response=>response.json())

fetch('https://swapi.dev/api/people').then(response=>response.json())
fetch('https://swapi.py4e.com/api/people').then(response=>response.json())


```
fetch(URL, {
  mode: 'cors',
  headers: {
    'Access-Control-Allow-Origin':'*'
  }
})
  .then(response => response.json())
  .then(data => {
 ```


Explication de l'origine (http...)
https://www.youtube.com/watch?v=0IMz8d9Cby4

Bonne définition, netscape
https://www.youtube.com/watch?v=Agu5dfWXQzA


## Intro
Si dans votre site vous avez utilisé une image d'une url externe et que vous avez une image cassée.
![image](https://user-images.githubusercontent.com/75088424/150318851-ede8c42e-3b5c-42b3-a354-4f5464312f58.png)
ou si votre site essaie de ramener des datas de votre API et que vous avez cette erreur
![erreurCors](https://user-images.githubusercontent.com/75088424/150319783-72f28081-499b-4e51-a993-fba9af69ca34.JPG)
C'est qu'il faut connaitre les cors! 

## intro bis
On peut appeler une api depuis n'importe quel url.
Ex google + api SW
fetch('https://swapi.dev/api/people').then(response=>response.json())

Parfait, je vais pouvoir récupérer toutes les données de datasquare
fetch('https://api.datasquare.analytics.safran').then(response=>response.json())

pas grave, il y a datahub
fetch('https://datahub-api.analytics.safran').then(response=>response.json())

Ca ne marche pas
Regardons l'erreur: "has been blocked by CORS policy"


QCM
C'est quoi un cors alors?
1 - ça fait mal au pied
2 - un mécanisme - une petit bout de code - pour accepter une requête cross origin (origine croisée)
3 - un formidable groupe de pop rock irlandais des années 2000



## à quoi ça sert un cors ?
(illustrations CORS in 100 Seconds)
C'est un mecanisme qui permet à un site web avec une url A de faire des requetes de datas sur d'autres url /serveur (B, C, D...). Sans cors chez B, C, D... lui autorisant l'accès, le site A ne peut faire que des requêtes vers son serveur A, un serveur de la même origine. 
On comprend son nom: «  Cross-origin resource sharing » (CORS) ou « partage des ressources entre origines multiples / croisées ». Le cors permet de faire des requêtes réussies sur Url / serveur d'origine B, C, D...

Le code est bien implémenté du coté serveur. Pourtant c'est dans le navigateur, du côté client que ça se passe. Depuis 1995, Netscape 2, les navigateur appliquent une règle de sécurité: "same-origin policy" (politique de même origine). les navigateurs, dans leur système de sécurité, ils autorisent donc un site web à demander librement des images et des datas depuis sa propre url. Mais bloque tout ce qui vient d'url externe sauf si certaines conditions sont réunies. A savoir la présence de cors chez A. 
Exemple avec Datasquare.
mais ça ne marche pas depuis la page!
fetch('https://api.datasquare.analytics.safran').then(response=>response.json())

Plus généralement, ça sert à se protéger des failles de sécurité, en particulier: Cross site request forgery / XSRF dit c-surf (falsification des requêtes inter sites)
Les requêtes XMLHttpRequest et l'API Fetch respectent la règle "same-origin policy" d'origine unique. Cela signifie qu'une application web qui utilise ces API peut donc uniquement émettre des requêtes vers la même origine que celle à partir de laquelle l'application a été chargée. Si elle veut émettre des requêtes vers d'autres origines, elles devront avoir un CORS qui l'y autorise.

Cors:" j'accepte une requete cross origin (origine multiple / croisée) dans ce ou ces cas particulier(s)". C'est ce que dit l'erreur (critikart)

On parle d'origine, c'est quoi l'origine? C'est la combinaisons protocole, domaine et port
Si l'un de ces 3 éléments change, l'origine n'est plus la même.

Il y a quelques exceptions (sur MDN comme une image cross origin)

### Comment ça marche ? 
MDN
https://developer.mozilla.org/fr/docs/Web/HTTP/CORS
Le mécanisme consiste à ajouter dans des en-têtes HTTP un ou des user-agent (=information échangée sous forme de chaîne de caractères, entre le navigateur utilisé par l'internaute et le serveur du site web visité) afin donc de permettre à un utilisateur d'accéder aux ressources d'un serveur situé sur une autre origine que le site courant. 
l'utilisateur réalise alors une requête HTTP multi-origine (cross-origin) sécurisés.

### 3 cas principaux: requête simple, requête necessitant une requête préliminaire et requêtes avec informations d'authentification (cookie)

#### requête simple

Le standard CORS fonctionne grâce à l'ajout de nouveaux en-têtes HTTP qui permettent aux serveurs de décrire un ensemble d'origines autorisées pour lire l'information depuis un navigateur web.
Acces-Control-Allow-Origin

#### requête necessitant une requête préliminaire

Pour les méthodes de requêtes HTTP qui entraînent des effets de bord sur les données côté serveur (notamment pour les méthodes en dehors de GET ou pour les méthodes POST utilisées avec certains types MIME), la spécification indique que les navigateurs doivent effectuer une requête préliminaire (« preflight request ») et demander au serveur les méthodes prises en charges via une requête utilisant la méthode OPTIONS puis, après approbation du serveur, envoyer la vraie requête. 
Acces-Control-Allow-Headers

#### requêtes avec informations d'authentification

Les serveurs peuvent également indiquer aux clients s'il est nécessaire de fournir des informations d'authentification (que ce soit des cookies ou des données d'authentification HTTP) avec les requêtes.
Par défaut les cookies sont bloqués. Dans la requête, la commande fetch, il faut ajouter credential include. Mais surtout, du côté de l'autre origine, il faut accepter dans le cors (credential à true).
Acces-Control-Allow-Credentials



(cors 100 sec)
Quand le navigateur fait une requête, il ajoute 




Vous avez déjà vu cette erreur? C'est un problème de cors.
AJAX

Le CORS permet de prendre en charge des requêtes multi-origines sécurisées et des transferts de données entre des navigateurs et des serveurs web. Les navigateurs récents utilisent le CORS dans une API contenante comme XMLHttpRequest ou Fetch pour aider à réduire les risques de requêtes HTTP multi-origines.

En effet
![image](https://user-images.githubusercontent.com/75088424/150301214-5ff2790b-36bd-4438-9661-ad5ed8ce28bc.png)


    Access-Control-Allow-Origin : quelle origine est autorisée ?
    Access-Control-Allow-Credentials : les requêtes sont-elles autorisées même si le Credentials Mode est réglé en include ?
    Access-Control-Allow-Headers : quels en-têtes peuvent être utilisés ?
    Access-Control-Allow-Methods : quelles méthodes de requête HTTP sont autorisées ?
    Access-Control-Expose-Headers : quels en-têtes peuvent être affichés ?
    Access-Control-Max-Age : quel est le délai de validité de la requête préliminaire ?
    Access-Control-Request-Headers : quel en-tête HTTP est spécifié dans la requête préliminaire ?
    Access-Control-Request-Method : quelle méthode HTTP est spécifiée dans la requête préliminaire ?
    Origin : quelle est la source de la requête ?

A quoi ça sert ? Où, quand et comment ?

Pourquoi c’est important ?

Cas pratique ? DataSquare ?
Avantages et inconvénients du CORS

En réalité, le CORS sert à contourner un certain réglage de base, à savoir la Same-Origin Policy. La SOP, représente quant à elle un moyen efficace de prévenir les connexions potentiellement dangereuses. Cependant, Internet est souvent basé sur de telles Cross-Origin Requests, en raison du grand nombre de demandes de connexion d’un hôte à un autre.

CORS offre donc une solution provisoire : des exceptions peuvent être créées à l'aide de CORS pour les situations dans lesquelles des Cross-Origin Requests sont explicitement requises. Toutefois, pour des raisons de commodité, il existe un risque que les exploitants de sites Web n'utilisent que des caractères wildcards qui permettraient d’annuler toute protection de la SOP. Il est donc important de n'utiliser CORS que dans certains cas particuliers, et de le configurer de manière aussi restrictive que possible.

CORS est-il une mauvaise chose ?

Comme pour les superpouvoirs, il s'agit de savoir comment les utiliser. Par conséquent, CORS n'est pas nécessairement une mauvaise chose. Nous avons vu dans de nombreux cas que CORS a un usage légitime, et c'est pourquoi il a été inventé et est devenu une norme Web en premier lieu. Cependant, vous devez être conscient de la configuration CORS que vous mettez en place sur votre serveur et des effets secondaires qu'elle a sur la sécurité.
Que dois-je prendre en compte ?

En gros, vous devez faire une distinction :

    Qui a un besoin légitime d'accès ? Peut-être n'y a-t-il qu'un site Web spécifique ou un petit ensemble de sites Web qui ont besoin d'un accès. Si c'est le cas, dressez-en la liste. Pour le dire autrement, vous ajoutez des sites web spécifiques à une "liste blanche" de domaines acceptés.
    Tous les points d'accès doivent-ils être exposés ? Examinez vos différents points d'extrémité et vous verrez peut-être qu'ils ont des utilisations légitimes différentes qui nécessitent des configurations CORS différentes.
    Quels sont les effets secondaires pour les points d'extrémité fournissant des données ? Certains points de terminaison, généralement les points de terminaison verbaux GET, fourniront des données mais ne modifieront rien dans l'état de votre serveur (ne modifieront pas l'état d'authentification ou les données stockées). Pour ces points d'extrémité, vérifiez si les données que vous fournissez sont confidentielles et si les origines CORS autorisées ont une raison légitime de les demander.
    Et les effets sur les points d'extrémité qui modifient les données ? D'autres points d'extrémité, généralement les points d'extrémité des verbes POST/DELETE/PUT, fournissent des données mais modifient également l'état de votre serveur. Dans ce cas, le risque est plus élevé car CORS peut être utilisé pour déclencher des actions involontaires, telles que la modification des données de l'utilisateur, la modification des informations de connexion, l'envoi d'e-mails, etc.
    Qu'en est-il des services tiers ? Si vous devez fournir une API à des tiers, il est bon que vous implémentiez l'autorisation d'une manière qui requiert le consentement de l'utilisateur. Par exemple, OAuth vous permet d'autoriser des sites Web et des applications tiers et requiert le consentement explicite de l'utilisateur.

