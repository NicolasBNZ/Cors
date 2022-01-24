# Les cors

https://www.youtube.com/watch?v=4KHiSt0oLJ0
preflight = contrôle en amont
https://blog.webdevsimplified.com/2021-05/cors/
https://www.youtube.com/watch?v=h-WtIT6gCBk
https://www.youtube.com/watch?v=irpWV4effNE


    https://datahub-api.analytics.safran

    https://api.datasquare.analytics.safran


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


## Qu’est ce qu’un cors ?
(illustrations CORS in 100 Seconds)
C'est un mecanisme - un petit bout de code - qui permet à un site web avec une url A /serveur A de faire des requetes de datas sur d'autres url /serveur (B, C, D...). Sans cors, le site A ne peut faire que des requêtes vers son serveur A, un serveur de la même origine. 
On comprend son nom: «  Cross-origin resource sharing » (CORS) ou « partage des ressources entre origines multiples ». Le cors permet de faire des requêtes réussies sur Url / serveur d'origine B, C, D...
C'est dans le navigateur que ça se passe. Depuis 1995, Netscape 2, les navigateur appliquent une règle de sécurité: "same-origin policy" (politique de même origine). les navigateurs, dans leur système de sécurité, ils autorisent donc un site web à demander librement des images et des dates depuis sa propre url. Mais bloque tout ce qui vient d'url externe sauf si certaines conditions sont réunies. A savoir la présence de cors chez A. Plus gnéralement, ça sert à se protéger des failles de sécurité, en particulier: Cross site request forgery / XSRF dit c-surf (falsification des requêtes inter sites)
Les requêtes XMLHttpRequest et l'API Fetch respectent la règle "same-origin policy" d'origine unique. Cela signifie qu'une application web qui utilise ces API peut donc uniquement émettre des requêtes vers la même origine que celle à partir de laquelle l'application a été chargée, sauf si des CORS sont utilisés.

Cors:" j'accepte une requete cross origin (origine multiple) dans ce ou ces cas particulier(s)". C'est ce que dit l'erreur (critikart)

On parle d'origine, c'est quoi l'origine? C'est la combinaisons protocole, domaine et port
Si l'un de ces 3 éléments change, l'origine n'est plus la même.


Il y a quelques exceptions (sur MDN comme une image cross origin)

### Comment ça marche ? 
MDN
https://developer.mozilla.org/fr/docs/Web/HTTP/CORS
Le mécanisme consiste à ajouter dans des en-têtes HTTP un ou des user-agent (=information échangée sous forme de chaîne de caractères, entre le navigateur utilisé par l'internaute et le serveur du site web visité) afin donc de permettre à un utilisateur d'accéder aux ressources d'un serveur situé sur une autre origine que le site courant. 
l'utilisateur réalise alors une requête HTTP multi-origine (cross-origin) sécurisés.

### 3 cas principaux: requête simple, requête necessitant une requête préliminaire et requêtes avec informations d'authentification (cookie)

Le standard CORS fonctionne grâce à l'ajout de nouveaux en-têtes HTTP qui permettent aux serveurs de décrire un ensemble d'origines autorisées pour lire l'information depuis un navigateur web. De plus, pour les méthodes de requêtes HTTP qui entraînent des effets de bord sur les données côté serveur (notamment pour les méthodes en dehors de GET ou pour les méthodes POST utilisées avec certains types MIME), la spécification indique que les navigateurs doivent effectuer une requête préliminaire (« preflight request ») et demander au serveur les méthodes prises en charges via une requête utilisant la méthode OPTIONS puis, après approbation du serveur, envoyer la vraie requête. Les serveurs peuvent également indiquer aux clients s'il est nécessaire de fournir des informations d'authentification (que ce soit des cookies ou des données d'authentification HTTP) avec les requêtes.

(cors 100 sec)
Quand le navigateur fait une requête, il ajoute 




Vous avez déjà vu cette erreur? C'est un problème de cors.
AJAX

Le CORS permet de prendre en charge des requêtes multi-origines sécurisées et des transferts de données entre des navigateurs et des serveurs web. Les navigateurs récents utilisent le CORS dans une API contenante comme XMLHttpRequest ou Fetch pour aider à réduire les risques de requêtes HTTP multi-origines.

En effet
![image](https://user-images.githubusercontent.com/75088424/150301214-5ff2790b-36bd-4438-9661-ad5ed8ce28bc.png)




A quoi ça sert ? Où, quand et comment ?

Pourquoi c’est important ?

Cas pratique ? DataSquare ?
