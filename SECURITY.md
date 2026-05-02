# Politique de Sécurité — VOANH AI

## Versions supportées

| Version | Support sécurité |
|---------|-----------------|
| Dernière version (`main`) | ✅ Activement maintenue |
| Versions antérieures | ❌ Non supportées |

---

## Signaler une Vulnérabilité

Si vous découvrez une faille de sécurité dans ce projet, **ne créez pas d'issue publique**.

**Procédure :**
1. Envoyez un e-mail à l'adresse du mainteneur (à renseigner dans ce fichier)
2. Décrivez précisément : nature du problème, étapes de reproduction, impact potentiel
3. Une réponse sera apportée sous **72 heures**
4. Un correctif sera publié sous **7 jours** pour les failles critiques

> Les rapports de bonne foi seront traités avec confidentialité. Aucune action légale ne sera engagée contre les chercheurs en sécurité agissant de manière responsable.

---

## Architecture de Sécurité

VOANH AI est une **Single Page Application 100 % côté client** (HTML + CSS + JS vanilla).
Il n'existe aucun backend, aucun serveur, aucune base de données distante.

### Ce que cela signifie concrètement

| Composant | Implémentation | Implication sécurité |
|-----------|---------------|----------------------|
| Clé API Mistral | Cookie navigateur (365j) + localStorage | Visible en DevTools — ne jamais partager la session |
| Conversations | IndexedDB locale | Jamais transmises à des tiers |
| Agents & Mémoire | IndexedDB locale | Stockage 100 % navigateur |
| Appels réseau | Uniquement vers `api.mistral.ai` | Aucun autre serveur contacté |

---

## Risques Connus et Mesures en Place

### 1. Exposition de la Clé API

**Risque** : La clé API Mistral est stockée dans le cookie et localStorage du navigateur.

**Impact** :
- En usage **local** : risque faible — seul l'utilisateur de la machine a accès
- En **hébergement public statique** (GitHub Pages, Netlify, etc.) sans proxy backend : risque **critique** si la clé est pré-remplie dans le code

**Mesure en place** :
- La clé n'est jamais écrite en dur dans le code source
- Chaque utilisateur saisit sa propre clé via le wizard au premier lancement
- Le `.gitignore` protège contre tout commit accidentel de fichiers `.env`

**Recommandation** : Utilisez VOANH AI en **usage local uniquement**. Tout hébergement public nécessite un proxy backend injectant la clé côté serveur.

---

### 2. Dépendances CDN sans SRI

**Risque** : Bootstrap 5.3.3 (CSS + JS) et Google Fonts sont chargés depuis des CDN sans attribut `integrity` (Subresource Integrity).

**Impact** : Si le CDN est compromis, du code malveillant pourrait être injecté.

**Mesure en place** :
- Une Content Security Policy (CSP) via balise `<meta>` restreint les origines autorisées
- `connect-src` est limité à `api.mistral.ai` uniquement

**Recommandation** : Pour un hébergement de production, remplacez les liens CDN par des copies locales des bibliothèques et ajoutez des hashes SRI vérifiés depuis les sources officielles :
- Bootstrap SRI : [getbootstrap.com](https://getbootstrap.com/docs/5.3/getting-started/download/)
- jsDelivr SRI : disponible sur chaque page de package jsDelivr

---

### 3. Injection XSS via `innerHTML`

**Risque** : L'application utilise `innerHTML` avec des données issues de l'API Mistral (noms d'agents, contenu de messages).

**Impact** : Si l'API Mistral retournait du HTML malveillant, il pourrait être interprété par le navigateur.

**Mesure en place** :
- La CSP restreint `script-src` aux sources connues + inline (nécessaire vu l'architecture)
- Les données utilisateur passent uniquement via l'API Mistral, qui n'est pas un vecteur d'injection classique

**Limitation** : `'unsafe-inline'` dans la CSP est requis car tous les scripts et styles sont inline dans `index.html`. La CSP ne protège donc pas contre le XSS DOM-based interne, mais elle empêche le chargement de scripts depuis des origines non autorisées.

---

### 4. Absence de Backend / Proxy

**Risque** : L'application contacte directement `api.mistral.ai` depuis le navigateur.

**Impact** : En usage local, ce design est intentionnel et sécurisé. En hébergement public, la clé API de l'hébergeur serait exposée côté client.

**Mesure en place** : Documenté explicitement dans le README — l'hébergement public sans proxy est déconseillé.

---

## Ce qui Est Hors Périmètre

Les éléments suivants ne sont **pas** dans le périmètre de cette politique de sécurité :

- Vulnérabilités dans l'infrastructure de Mistral AI (`api.mistral.ai`)
- Vulnérabilités dans Bootstrap ou Google Fonts
- Attaques nécessitant un accès physique à la machine de l'utilisateur
- Attaques par ingénierie sociale visant à obtenir la clé API directement auprès de l'utilisateur

---

## Bonnes Pratiques pour les Utilisateurs

1. **Ne jamais pré-remplir** la clé API dans le code source ou dans une version partagée de `index.html`
2. **Ne jamais committer** `index.html` si vous y avez manuellement injecté votre clé
3. **Révoquer immédiatement** toute clé suspectée compromise sur [console.mistral.ai](https://console.mistral.ai) → API Keys → Delete
4. **Utiliser une clé dédiée** à VOANH AI avec des quotas limités si possible
5. **Ne pas ouvrir** VOANH AI sur un appareil partagé ou non de confiance
