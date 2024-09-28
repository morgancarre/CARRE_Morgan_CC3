# CARRE_Morgan_CC3

    Question 1.1 donner la liste des en-têtes de la réponse HTTP du serveur.

        Connection : keep-alive
        Date:Wed, 25 Sep 2024 02:18:46 GMT
        Keep-Alive:timeout=5
        Transfer-Encoding: chunked

    Question 1.2 donner la liste des en-têtes qui ont changé depuis la version précédente.

        Connection:keep-alive
        Content-Length:20
        Content-Type:application/json
        Date:Wed, 25 Sep 2024 02:23:24 GMT
        Keep-Alive:timeout=5

        La page est afficher sous forme json .

    Question 1.3 Que contient la réponse reçue par le client ?

        Le client ne reçois rien à cause d'un erreur serveur.
    
    Question 1.4 Quelle est l'erreur affichée dans la console ? Retrouver sur https://nodejs.org/api le code d'erreur affiché.

        L'erreur ENOENT s'affiche parce que le fichier passé dans `fs.readFile()` n'a pas été trouvé. En le renommant en "index.html" l'erreur disparaît.

    Question 1.5 Donner le code de requestListener() modifié avec gestion d'erreur en async/await.

        async function requestListener(_request, response) {
            try {
                const contents = await fs.readFile("index.html", "utf8");
                response.setHeader("Content-Type", "text/html");
                response.writeHead(200);
                return response.end(contents);
            } catch(error) {
                console.error(error);
                response.writeHead(500);
                return response.end("<html><h1>Erreur 500<h1></html>");
            }
        }


    Question 1.6 indiquer ce que cette commande a modifié dans votre projet.

        Ces commandes ont installés 2 packaages : cross-env et nodemon. cross-env qui aide à gérer les variables d'environnement sous Windows, et nodemon refresh automatiquement le serveur lorsque des fichiers sont changés.

    Question 1.7 Quelles sont les différences entre les scripts http-dev et http-prod ?

        Avec http-dev, le serveur est lancé à l'aide de nodemon ce qui fait une mise à jour automatique à chaque modification de fichier (avec la commande console.log("NODE_ENV =", process.env.NODE_ENV); qui s'affiche dès qu'on ajoute dans notre fichier : server-http.mjs et qu'on l'enregistre).http-prod démarre le serveur de manière classique sans actualisation automatique, ça permet la mise en service du serveur.


    Question 1.8 donner les codes HTTP reçus par votre navigateur pour chacune des quatre pages précédent

        localhost:8000/index.html:200

        localhost:8000/random.html:200

        localhost:8000/:404
        
        localhost:8000/dont-exist:404

    Question 2.1 Donner les URL des documentations de chacun des modules installés par la commande précédente.
        loglevel : https://www.npmjs.com/package/loglevel 
        morgan : https://www.npmjs.com/package/morgan
        Express.js : https://expressjs.com/en/4x/api.html 
        http-errors : https://www.npmjs.com/package/http-errors 

    Question 2.2 Vérifier que les trois routes fonctionnent.
        Les trois routes fonctionnent correctement. Les routes / et /index.html présentent le contenu du fichier index.html, tandis que la route /random/:nb renvoie nb nombres aléatoires.

    Question 2.3 Lister les en-têtes des réponses fournies par Express. Lesquelles sont nouvelles par rapport au serveur HTTP ?
        Routes / et /index.html :

        Accept-Ranges: bytes
        Cache-Control: public, max-age=0
        Connection: keep-alive
        Content-Length: 903
        Content-Type: text/html; charset=UTF-8
        Date: Sat, 28 Sep 2024 18:45:34 GMT
        Etag: W/"39-bb0851422df09"
        Keep-Alive: timeout=5
        Last-Modified: Sat, 28 Sep 2024 17:52:40 GMT
        X-Powered-By: Express

        Route /random/nb :

        Connection: keep-alive
        Content-Length: 45
        Content-Type: text/html; charset=utf-8
        Date: WSat, 28 Sep 2024 18:47:20 GMT
        Etag: W/"f362950ddd46ec6dd41f30b184b2139d"
        Keep-Alive: timeout=5
        X-Powered-By: Express

        Les nouveautés sont : l'apparition de "Etag" et de "X-Powered-By: Express"

    Question 2.4 Quand l'événement listening est-il déclenché ?
        L'événement "listening" se produit lorsque le serveur Express.js commence à écouter sur le port spécifié et est prêt à recevoir des requêtes HTTP.

    Question 2.5 Indiquer quelle est l'option (activée par défaut) qui redirige / vers /index.html ?
        La propriété index : 
        app.use(express.static("static", {index:false}));

    Question 2.6 Visiter la page d'accueil puis rafraichir (Ctrl+R) et ensuite forcer le rafraichissement (Ctrl+Shift+R). Quels sont les codes HTTP sur le fichier style.css ? Justifier.
        En effectuant un Ctrl+R, on reçoit un code HTTP 304, indiquant que la page n'a pas changé par rapport à la version en cache. En revanche, en utilisant Ctrl+Shift+R, on obtient un code HTTP 200, car ça rafraîchit la page en ignorant le cache.

    Question 2.7 Vérifier que l'affichage change bien entre le mode production et le mode development.
        L'affichage diffère : en mode développement, l'erreur est entièrement visible tandis qu'en mode production elle est masquée.