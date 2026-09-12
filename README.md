# Assistant IA Discord — Discloud

Bot Discord qui :

- répond quand on le mentionne dans un serveur ;
- répond à tous les messages privés qui lui sont envoyés ;
- affiche ses réponses dans des embeds sans couleur ;
- ajoute un menu déroulant quand la réponse contient plusieurs choix ;
- mémorise brièvement le contexte de chaque conversation en mémoire ;
- répond uniquement à partir du programme Greendale en Mouvement fourni ;
- refuse les questions hors sujet ;
- limite chaque utilisateur à 20 messages ou choix toutes les 5 minutes.

Le document de référence est conservé dans `programme.pdf` et dans sa version
texte `programme.txt`, utilisée par le bot au démarrage.

## Déploiement avec Railway

1. Crée un projet Railway depuis le dépôt GitHub `Emil518/ATN`.
2. Dans **Variables**, ajoute :

   - `DISCORD_TOKEN` : le token de ton application Discord ;
   - `GEMINI_API_KEY` : la clé API du modèle.

3. Railway détectera le projet Node.js et utilisera `npm start`.
4. Vérifie les logs : le bot doit afficher qu'il est connecté.

Les secrets Replit et GitHub ne sont pas automatiquement transmis à Railway.
Ils doivent être ajoutés dans les variables privées du service Railway. Ne les
mets jamais dans `index.js`, `README.md`, un commit ou un fichier ZIP.

## Installation sur Discloud

1. Compresse le contenu de ce dossier en ZIP. Le fichier `index.js` doit être à la racine de l'archive.
2. Envoie le ZIP sur Discloud.
3. Dans les variables secrètes / variables d'environnement de Discloud, ajoute :

   - `DISCORD_TOKEN` : le token de ton application Discord ;
   - `GEMINI_API_KEY` : la clé API du modèle.

4. Active l'intent **Message Content** dans le [Discord Developer Portal](https://discord.com/developers/applications).
5. Invite le bot avec les permissions `View Channel`, `Send Messages`, `Embed Links` et `Read Message History`.
6. Démarre ou redémarre le bot.

Les secrets ne sont volontairement pas inclus dans le ZIP. Ne les mets pas dans
`README.md`, `.env.example` ou `index.js`.

## Variables facultatives

| Variable | Valeur par défaut | Utilité |
| --- | --- | --- |
| `GEMINI_MODEL` | `gemini-2.0-flash` | Modèle utilisé |
| `BOT_NAME` | `Assistant` | Nom utilisé dans les consignes internes |
| `BOT_LANGUAGE` | `français` | Langue par défaut |
| `MAX_HISTORY` | `12` | Nombre maximal de messages conservés par conversation |
| `RATE_LIMIT_MAX` | `20` | Nombre maximal de demandes par utilisateur |
| `RATE_LIMIT_WINDOW_MINUTES` | `5` | Durée de la fenêtre de quota |

## Tester en local

```bash
npm install
cp .env.example .env
# remplis .env uniquement sur ta machine
npm start
```

Le bot ne répond pas à tous les messages d'un serveur : il attend une
mention pour éviter le spam. En message privé, il répond directement.