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

