# Les cors

https://www.youtube.com/watch?v=4KHiSt0oLJ0
preflight = contrôle en amont
https://blog.webdevsimplified.com/2021-05/cors/
https://www.youtube.com/watch?v=h-WtIT6gCBk
https://www.youtube.com/watch?v=irpWV4effNE


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
C'est un mecanisme - un petit bout de code - qui permet à un site web avec une url A de faire des requetes de datas sur d'autres url (B, C, D...). Sans cors, le site A ne peut faire que des requêtes vers son serveur A, un serveur de la même origine. 
On comprend son nom: «  Cross-origin resource sharing » (CORS) ou « partage des ressources entre origines multiples ». Le cors permet de faire des requêtes réussies sur Url / serveur d'origine B, C, D...
C'est dans le navigateur que ça se passe. Depuis 1995, Netscape 2, les navigateur appliquent une règle de sécurité: "same-origin policy" (politique de même orgine). les navigateurs, dans leur système de sécurité, ils autorisent donc un site web à demander librement des images et des dates depuis sa propre url. Mais bloque tout ce qui vient d'url externe sauf si certaines conditions sont réunies. A savoir la présence de cors chez A.

Cors:" j'accepte une requete cross origin / origine multiple dans ce cas particulier". C'est ce que dit l'erreur (critikart)

protocole, port et domaine
Exception (sur MDN comme une image cross origin)

### Comment ça marche en théorie ? 
MDN
https://developer.mozilla.org/fr/docs/Web/HTTP/CORS
Le CORS est un mécanisme qui consiste à ajouter des en-têtes HTTP afin de permettre à un utilisateur d'accéder à des ressources d'un serveur situé sur une autre origine que le site courant. Un utilisateur réalise une requête HTTP multi-origine (cross-origin) lorsqu'il demande une ressource provenant d'un domaine, d'un protocole ou d'un port différent de ceux utilisés pour la page courante.

Pour des raisons de sécurité, les requêtes HTTP multi-origine émises depuis les scripts sont restreintes. Ainsi, XMLHttpRequest et l'API Fetch respectent la règle d'origine unique. Cela signifie qu'une application web qui utilise ces API peut uniquement émettre des requêtes vers la même origine que celle à partir de laquelle l'application a été chargée, sauf si des en-têtes CORS sont utilisés.

![image](https://user-images.githubusercontent.com/75088424/150316751-848d8233-1350-4503-9882-3619e4bf75fd.png)

Le CORS permet de prendre en charge des requêtes multi-origines sécurisées et des transferts de données entre des navigateurs et des serveurs web. Les navigateurs récents utilisent le CORS dans une API contenante comme XMLHttpRequest ou Fetch pour aider à réduire les risques de requêtes HTTP multi-origines.






Vous avez déjà vu cette erreur? C'est un problème de cors.
AJAX

En effet
![image](https://user-images.githubusercontent.com/75088424/150301214-5ff2790b-36bd-4438-9661-ad5ed8ce28bc.png)




A quoi ça sert ? Où, quand et comment ?

Pourquoi c’est important ?

Cas pratique ? DataSquare ?
