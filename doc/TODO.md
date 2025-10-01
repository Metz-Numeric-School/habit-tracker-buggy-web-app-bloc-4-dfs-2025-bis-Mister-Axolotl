# TODO

Suite à un audit effectué en amont, voici les failles et les bugs qui ont été identifés comme prioritaire.

## FAILLES

Légende

- ✅ Corrigé
- ⌛Je sais comment faire mais pas eu le temps
- ❌ Pas fait du tout

Les failles

* ✅ Des utilsateurs non admin ont des accès à l'interface de gestion des utilisateurs
* ✅ Les mots de passes ne sont pas chiffrée en base de données...
* ⌛ Des injections de type XSS ont été détéctées sur certains formulaires
-> Il suffit d'utiliser htmlSpecialchars()
* ⌛ On nous a signalé des injections SQL lors de la création d'une nouvelles habitudes
-> Il suffit d'utiliser les requêtes préparées avec prepare()
  * exemple dans le champs "name" : foo', 'INJECTED-DESC', NOW()); --

## BUGS

* ⌛ Une 404 est détéctée lors de l'accès à l'URL ``/habit/toggle``
-> l'api n'existe pas dans /Api et il faut ajouter le route dans routes.json
* ❌ Fatal error: Uncaught Error: Class "App\Controller\Api\HabitsController" lorsque l'on accède à l'URL  ``/api/habits``

**ATTENTION : certains bugs n'ont pas été listé**
