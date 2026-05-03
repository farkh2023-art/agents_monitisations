# VOANH AI — Chatbot LLM Free Tier Mistral Évolué

**VOANH AI** est une plateforme d'intelligence artificielle personnelle avancée, entièrement contenue dans **une seule page HTML**. Elle exploite la puissance des modèles **Mistral AI** via leur **Free Tier** généreux, offrant des capacités de chatbot sophistiquées avec mémoire globale, agents spécialisés auto-générés, et gestion complète des données — le tout en local, sans serveur backend.

---

## 🌟 Pourquoi VOANH AI est un Chatbot LLM Évolué ?

Contrairement aux chatbots basiques, VOANH AI intègre des fonctionnalités avancées directement dans son code source :

### 🔧 Architecture Technique Avancée

1. **Single Page Application (SPA) Autonome**
   - Tout le code tient dans **un seul fichier `index.html`** (≈ 3800 lignes)
   - Aucune dépendance serveur : HTML + CSS + JavaScript vanilla
   - Bootstrap 5.3 pour l'UI, Google Fonts pour la typographie cyberpunk
   - IndexedDB intégré pour le stockage local persistant

2. **Intégration Native Mistral AI**
   - Appel direct à l'API `https://api.mistral.ai/v1/chat/completions`
   - Support de **20+ modèles Mistral** (Omega, Zenith, Codestral, Devstral, Pixtral, Voxtral, etc.)
   - Gestion intelligente des tokens et du contexte (jusqu'à 375K tokens)
   - Températures adaptatives par modèle (0.42 à 1.44)

3. **Système de Mémoire Globale Persistante**
   - Base de données IndexedDB (`VOANH_AI_DB`) avec 4 stores : `chats`, `agents`, `global_memory`, `settings`
   - La mémoire n'est pas limitée au contexte de conversation : elle persiste entre les sessions
   - Recherche sémantique simplifiée par mots-clés et tags
   - Chaque message peut être sauvegardé manuellement dans la mémoire globale

4. **Génération Automatique d'Agents par IA**
   - Un agent n'est pas un simple preset : c'est une entité autonome générée par **Mistral Large**
   - Le wizard initial utilise un prompt sophistiqué pour créer **20 agents spécialisés** adaptés à votre profil
   - Chaque agent possède : nom, description, instructions détaillées, tags, style de réponse, température personnalisée
   - Les agents sont stockés localement et peuvent être modifiés, dupliqués, exportés

5. **Sécurité & Confidentialité**
   - La clé API Mistral est stockée dans un **cookie (365 jours)** + localStorage en fallback — **uniquement côté navigateur**
   - **Aucune donnée ne transite vers des serveurs tiers** — uniquement vers `api.mistral.ai`
   - Toutes les conversations, agents et mémoires restent sur votre navigateur
   - **Note importante** : en usage local, la clé API est protégée par votre session navigateur ; en hébergement public sans proxy backend, elle serait accessible à d'autres utilisateurs — voir la section [Sécurité](#️-sécurité--risque-dexposition-de-la-clé-api)

---

## 🚀 Comment Obtenir Votre Clé API Mistral

### Étape 1 : Créer un Compte Mistral AI

1. Rendez-vous sur **[console.mistral.ai](https://console.mistral.ai)**
2. Cliquez sur **"Sign Up"** ou **"Get Started for Free"**
3. Inscrivez-vous avec votre email ou via GitHub/Google

### Étape 2 : Générer Votre Clé API

1. Une fois connecté, accédez à votre **Tableau de Bord (Dashboard)**
2. Dans le menu latéral, cliquez sur **"API Keys"**
3. Cliquez sur **"Create New Key"**
4. Donnez un nom à votre clé (ex: `VOANH-Personal`)
5. **Copiez immédiatement la clé** — elle ne sera affichée qu'une seule fois !
   - Format : `votre_clé_commence_par_` suivi de caractères alphanumériques

### Étape 3 : Vérifier Vos Quotas Free Tier

Mistral offre un **Free Tier généreux** :
- **Gratuit** : Pas de carte bancaire requise
- **Quotas mensuels** : Suffisants pour un usage personnel intensif
- **Modèles inclus** : Mistral Small, Medium, Large, Codestral, Pixtral, etc.
- **Suivi en temps réel** : Consultez `console.mistral.ai → Dashboard` pour voir vos quotas restants

> 💡 **Astuce** : Le Free Tier Mistral est idéal pour le développement et l'usage personnel. Pour un usage professionnel intensif, passez à un plan payant.

---

## ⚠️ Sécurité — Risque d'Exposition de la Clé API

> Pour signaler une vulnérabilité ou consulter la politique de sécurité complète, voir [SECURITY.md](./SECURITY.md).

> **AVERTISSEMENT IMPORTANT** : VOANH AI est une application **100 % côté client** (HTML/JS pur). La clé API Mistral que vous saisissez est stockée dans le **cookie de votre navigateur** et dans **localStorage** — elle ne quitte jamais votre appareil vers un serveur tiers, mais elle reste **lisible par quiconque a accès physique ou logiciel à votre navigateur**.

### Ce que cela implique concrètement

| Scénario | Risque | Recommandation |
|----------|--------|----------------|
| Usage local sur votre PC personnel | Faible | ✅ Méthode recommandée |
| Hébergement public (GitHub Pages, Netlify…) sans backend | **Élevé** | ❌ Ne jamais pré-configurer votre clé dans le code |
| Hébergement public avec backend sécurisé (proxy API) | Maîtrisé | ⚠️ Voir section dédiée ci-dessous |
| Partage du fichier `index.html` avec votre clé incluse | **Critique** | ❌ Ne jamais partager le fichier avec votre clé |

### Bonnes pratiques

- **Ne jamais écrire votre clé API en clair dans le code source**
- **Ne jamais versionner** (git commit) un fichier contenant votre clé
- Si vous suspectez une exposition, **révoquez immédiatement** la clé sur [console.mistral.ai](https://console.mistral.ai) → API Keys → Delete
- Chaque utilisateur doit saisir **sa propre clé** au premier lancement via le wizard

---

## 📦 Installation

### Méthode 1 — Usage Local (Recommandée) ✅

L'usage local est la méthode la plus sûre. Votre clé API reste confinée à votre propre navigateur, sur votre machine.

**Étapes :**

1. **Téléchargez** le fichier `index.html` depuis ce dépôt
2. **Enregistrez-le** sur votre ordinateur (bureau, dossier dédié, clé USB)
3. **Ouvrez-le** directement dans votre navigateur (Chrome, Firefox, Edge ou Safari)
   ```
   Exemple : double-clic sur index.html
   ```
4. **Configurez** votre clé API Mistral au premier lancement via le wizard intégré

> **Aucune installation de dépendances requise** — pas de `npm`, `pip`, ni build system. Un seul fichier suffit.

---

### Méthode 2 — Hébergement Public avec Backend Sécurisé ⚠️

> **Cette méthode est uniquement recommandée pour des équipes ou des déploiements multi-utilisateurs maîtrisés.** Elle nécessite un backend serveur agissant comme proxy entre le navigateur et l'API Mistral, afin que la clé API ne soit jamais exposée côté client.

**Architecture requise :**

```
Navigateur (index.html) → Votre serveur proxy → api.mistral.ai
```

**Ce que le proxy doit faire :**
- Recevoir les requêtes du client (sans clé API)
- Injecter la clé API côté serveur (variable d'environnement `MISTRAL_API_KEY`)
- Transmettre la requête à `api.mistral.ai`
- Retourner la réponse au client

**Exemple de variable d'environnement à configurer sur votre serveur :**
```
MISTRAL_API_KEY=votre_clé_ici   # Ne jamais committer cette valeur
```

> **Sans ce proxy, ne déployez jamais VOANH AI sur un hébergement public accessible à des tiers.**  
> GitHub Pages, Netlify et Vercel sont des hébergements statiques : ils ne peuvent pas protéger votre clé API. Chaque visiteur aura accès à votre clé si elle est incluse dans le code.

---

### Configuration Initiale (Wizard Intégré)

Au premier lancement, un **wizard en 3 étapes** vous guide automatiquement :

**Étape 1 — Clé API Mistral**
- Saisissez votre clé API (minimum 20 caractères)
- La clé est validée puis stockée dans un cookie (365 jours) + localStorage
- Le statut **ONLINE** s'affiche immédiatement si la clé est valide
- **Ne saisissez que votre propre clé** — ne partagez jamais ce fichier avec une clé pré-remplie

**Étape 2 — Personnalisation de votre IA**
- Donnez un nom à votre assistant (ex : `JARVIS`, `ATHENA`, `CODEX`)
- Définissez son objectif principal (ex : `"Assistant de développement full-stack"`)

**Étape 3 — Génération automatique des agents**
- Mistral Large analyse votre profil utilisateur
- **20 agents spécialisés** sont créés automatiquement et adaptés à vos besoins
- Une preview des agents générés est affichée avant validation

---

## 🏠 Avantages de l'Usage Local (Méthode Recommandée)

### 🔒 Confidentialité et Sécurité Maximales
- **Aucun serveur backend** : Vos données ne quittent jamais votre navigateur
- **Clé API protégée** : Stockée localement dans votre navigateur, jamais transmise à des tiers
- **Risque d'exposition nul** : Contrairement à un hébergement public statique, personne d'autre ne peut accéder à votre clé
- **Conformité RGPD** : Pas de collecte de données, pas de tracking

### ⚡ Performance & Réactivité
- **Chargement instantané** : Pas de requêtes serveur hormis l'API Mistral
- **Interface fluide** : CSS optimisé, animations hardware-accelerated
- **Mode offline partiel** : L'interface fonctionne sans connexion (seules les requêtes IA nécessitent internet)

### 💾 Persistance des Données
- **IndexedDB** : Base de données locale robuste (jusqu'à plusieurs Go selon le navigateur)
- **Sauvegarde automatique** : Chaque message, agent et mémoire est persisté immédiatement
- **Export/Import** : Sauvegardez toutes vos données dans un fichier JSON

### 🛠️ Flexibilité Totale
- **Personnalisation illimitée** : Modifiez le CSS, les prompts, les modèles
- **Pas de dépendances** : Aucun npm, pip, ou build system requis
- **Portable** : Copiez-collez le fichier sur une clé USB, utilisez-le partout

---

## 🆓 Avantages du Moteur Free Tier Mistral

### 🎯 Gratuité Réelle
- **Aucune carte bancaire** requise pour commencer
- **Quotas mensuels renouvelés** gratuitement
- **Idéal pour** : Développement, tests, usage personnel, prototypes

### 🧠 Modèles Haute Performance
| Modèle | Force Principale | Contexte | Usage Recommandé |
|--------|------------------|----------|------------------|
| **Mistral Omega (Large)** | Raisonnement complexe | 4M tokens | Analyses profondes, code avancé |
| **Mistral Zenith (Medium)** | Ratio qualité/vitesse | 375K tokens | Usage quotidien polyvalent |
| **Codestral / Devstral** | Génération de code | 4M tokens | Développement, debugging |
| **Pixtral** | Vision par ordinateur | 4M tokens | Analyse d'images, OCR |
| **Voxtral** | Traitement audio | 4M tokens | Transcription, analyse sonore |
| **Mistral Flash (Small)** | Rapidité extrême | 4M tokens | Réponses instantanées |

### 📈 Évolutivité
- **Upgrade seamless** : Passez à un plan payant sans changer de code
- **Multi-modèles** : Switch instantané entre 20+ modèles selon la tâche
- **Contexte étendu** : Jusqu'à 375K tokens pour analyser des documents longs

### 🌍 Écosystème Open
- **Documentation complète** : [docs.mistral.ai](https://docs.mistral.ai)
- **SDK officiels** : Python, Node.js, TypeScript
- **Communauté active** : Discord, GitHub, forums dédiés

---

## 🧠 La Mémoire Globale : Votre Cerveau Numérique Persistant

### Concept

La **Mémoire Globale** est un système révolutionnaire qui dépasse le contexte limité des conversations. Contrairement à la mémoire temporaire d'un chat classique (qui disparaît après chaque session), la mémoire globale de VOANH AI :

- **Persiste indéfiniment** dans IndexedDB
- **Est partagée** entre toutes vos conversations
- **Peut être consultée** à tout moment via le panneau latéral
- **Enrichit les réponses** de l'IA en injectant du contexte pertinent

### Fonctionnement Technique

```javascript
const memory = {
  add: async (content, tags = []) => {
    // Crée une entrée avec id unique, timestamp, importance
    // Stocke dans IndexedDB (store: 'global_memory')
    // Met à jour l'état local et réaffiche la liste
  },
  getAll: async () => {
    // Charge toutes les mémoires depuis IndexedDB
  },
  getRelevant: (query, limit = 5) => {
    // Algorithme de scoring :
    // - +2 points si le contenu contient le mot-clé
    // - +1 point si un tag correspond
    // - +1 point par niveau d'importance
    // Retourne les top N mémoires formatées
  }
};
```

### Utilisation Pratique

#### Ajouter une Mémoire Manuellement
1. Cliquez sur le bouton **⬡ MÉMOIRE** en bas à droite
2. Saisissez un fait important dans le champ input
3. Appuyez sur **+** ou Entrée
4. Exemple : `"L'utilisateur préfère Python pour le backend et React pour le frontend"`

#### Sauvegarder une Réponse de l'IA
1. Après une réponse pertinente, cliquez sur **⬡ MÉMO** sous le message
2. Le contenu (tronqué à 200 caractères) est ajouté automatiquement
3. Toast de confirmation : "Ajouté à la mémoire globale"

#### Consulter la Mémoire
- Panneau latéral droit : liste des **12 dernières mémoires**
- Chaque entrée affiche : contenu + bouton **✕** pour suppression
- Code couleur : violet pour les tags, cyan pour les actions

### Exemple Concret

**Scénario** : Vous développez une application web

1. **Session 1** (Lundi) :
   - Vous dites : "Je crée une app de e-commerce avec Next.js"
   - Vous sauvegardez en mémoire : `"Projet: e-commerce Next.js + Stripe"`

2. **Session 2** (Mercredi) :
   - Vous demandez : "Comment intégrer le paiement ?"
   - L'IA récupère automatiquement la mémoire : `[MEM:projet] Projet: e-commerce Next.js + Stripe`
   - Réponse contextualisée : "Pour votre projet e-commerce Next.js, voici comment intégrer Stripe..."

3. **Session 3** (Vendredi) :
   - Panneau mémoire ouvert : vous voyez tous les faits importants
   - Vous supprimez une mémoire obsolète avec **✕**
   - Vous ajoutez : `"Le client veut un design dark mode cyberpunk"`

---

## 🤖 Création Automatique d'Agents

### Philosophie

Un **Agent** dans VOANH AI n'est pas un simple preset de prompt. C'est une **entité autonome** avec :
- Une **personnalité** définie
- Un **domaine d'expertise** spécialisé
- Des **règles comportementales** strictes
- Un **style de réponse** personnalisé
- Une **température** adaptée à sa tâche

### Processus de Génération Automatique

Lors du premier lancement (ou via le bouton **"✦ GÉNÉRER + D'AGENTS"**), le système :

1. **Analyse votre profil** via le nom et l'objectif saisis
2. **Appelle Mistral Large** avec un prompt sophistiqué :

```javascript
async function generateAgentsWithMistral(apiKey, aiName, aiGoal) {
  const prompt = `Tu es un expert en IA et en architecture de systèmes multi-agents.

L'utilisateur veut créer une IA personnelle nommée "${aiName}" avec l'objectif suivant :
"${aiGoal}"

Génère EXACTEMENT 20 agents spécialisés parfaitement adaptés à ce contexte.
Chaque agent doit avoir une spécialité unique et complémentaire des autres.

Réponds UNIQUEMENT avec un JSON valide...`;

  const res = await fetch("https://api.mistral.ai/v1/chat/completions", {
    method: "POST",
    headers: { "Authorization": `Bearer ${apiKey}`, "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "mistral-large-2512",
      messages: [{ role: "user", content: prompt }],
      temperature: 0.8,
      max_tokens: 8000
    })
  });
  
  // Parse la réponse JSON et retourne les 20 agents
}
```

3. **Parse la réponse JSON** de Mistral
4. **Stocke chaque agent** dans IndexedDB avec un UUID unique
5. **Affiche une preview** des 20 agents générés

### Exemple de Génération

**Profil Utilisateur** :
- Nom : `DEVBOX`
- Objectif : "Assistant de développement full-stack spécialisé en React, Node.js et DevOps"

**Agents Générés (extrait)** :

| Agent | Spécialité | Description |
|-------|------------|-------------|
| **ReactArchitect** | Frontend React | Expert en architecture React, hooks avancés, optimisation des performances |
| **NodeGuardian** | Backend Node.js | Maître des APIs REST/GraphQL, gestion de bases de données, sécurité |
| **DevOpsCommander** | CI/CD & Cloud | Spécialiste Docker, Kubernetes, GitHub Actions, déploiements AWS/Azure |
| **CodeAuditor** | Review & Qualité | Analyse statique, détection de bugs, suggestions de refactoring |
| **DBWizard** | Bases de données | SQL/NoSQL, optimisation de requêtes, modélisation de schémas |
| **SecuritySentinel** | Cybersécurité | Audit de vulnérabilités, bonnes pratiques OWASP, chiffrement |
| **UXOptimizer** | Expérience utilisateur | Accessibilité, performance perçue, design systems |
| **TestMaster** | Tests & QA | Unit tests, E2E, TDD, coverage analysis |
| ... | ... | ... (12 autres agents) |

Chaque agent inclut :
- **Instructions détaillées** (200-400 mots)
- **Tags** pour catégorisation
- **Style de réponse** (concis, détaillé, formel, créatif, pédagogique)
- **Température** adaptée (0.4 pour le code, 0.8 pour la créativité)

---

## 🎯 Utilisation des Agents

### Activer un Agent

1. Cliquez sur le bouton **⚙ AGENT** dans le header
2. Dans la modale, vous voyez :
   - **Liste des agents existants** (avec nom, description, actions)
   - **Boutons** : Importer, Générer + d'agents
   - **Formulaire** de création manuelle
3. Cliquez sur un agent dans la liste pour l'**activer immédiatement**
4. Ou sélectionnez-le via le dropdown **◈ NOM_AGENT** dans le header

### Effet d'un Agent Activé

Une fois activé, l'agent modifie le **prompt système** de toutes vos réponses :

```javascript
function buildSystemPrompt() {
  let prompt = "Tu es un assistant IA utile, précis et respectueux.";
  
  if (state.agent) {
    prompt += `\n\n[AGENT ACTIF: ${state.agent.name}]\n`;
    prompt += `Description: ${state.agent.desc}\n`;
    prompt += `Instructions spéciales:\n${state.agent.instructions}\n`;
    if (state.agent.primer) prompt += `\nNote personnelle: ${state.agent.primer}\n`;
    if (state.agent.forbidden) prompt += `\nInterdictions: ${state.agent.forbidden}\n`;
  }
  
  // Injection de la mémoire globale pertinente
  const lastUserMsg = state.messages.filter(m=>m.role==='user').pop()?.content || "";
  const relevantMemories = memory.getRelevant(lastUserMsg, 5);
  if (relevantMemories.length) {
    prompt += "\n\n[MÉMOIRE GLOBALE PERTINENTE]\n" + relevantMemories.join('\n');
  }
  
  return prompt;
}
```

### Changer d'Agent en Cours de Conversation

- **Sans perdre l'historique** : Switch instantané via le dropdown
- **Adaptation contextuelle** : Le nouvel agent reprend le fil avec sa personnalité
- **Exemple** :
  - Vous discutez avec **ReactArchitect** d'un composant
  - Vous switch sur **DevOpsCommander** pour déployer l'app
  - Vous switch sur **CodeAuditor** pour reviewer le code

### Créer un Agent Manuellement

Dans la modale Agent, remplissez :

1. **Nom** : Court et évocateur (ex: `BioInfoGPT`)
2. **Description** : Spécialité en 1 phrase
3. **Instructions** : Comportement détaillé (ex: "Réponds toujours en français, cite tes sources...")
4. **Tags** : Mots-clés pour recherche (ex: `biologie, génomique, médecine`)
5. **Modèle préféré** : Quel modèle utiliser par défaut avec cet agent
6. **Primer** : Phrase d'introduction type
7. **Avancé** :
   - Température (0 = déterministe, 2 = très créatif)
   - Style de réponse
   - Interdictions (ex: "Ne jamais donner de conseils médicaux directs")

### Actions sur les Agents

| Action | Description |
|--------|-------------|
| **✎ Modifier** | Éditez nom, description, instructions, settings |
| **⎘ Dupliquer** | Créez une copie pour itérer rapidement |
| **⬇ Exporter** | Téléchargez l'agent en fichier JSON |
| **✕ Supprimer** | Effacez définitivement l'agent |
| **⬆ Importer** | Chargez un agent depuis un fichier JSON |

---

## 📊 Utilisation des Data (Conversations, Mémoires, Agents)

### Architecture de Stockage

VOANH AI utilise **IndexedDB** avec 4 stores :

```javascript
const DB_NAME = "VOANH_AI_DB";
const DB_VERSION = 3;

// Stores :
// 1. 'chats' : { id, model, agentId, messages[], title, updated, fav }
// 2. 'agents' : { id, name, desc, instructions, tags, style, temperature, primer, forbidden, created }
// 3. 'global_memory' : { id, content, tags[], created, importance }
// 4. 'settings' : { id, value } (ex: aiConfig, currentChatId)
```

### Navigation dans les Archives

1. Cliquez sur le bouton **📦 ARCHIVES** en bas à gauche
2. Panneau latéral avec :
   - **Barre de recherche** : Filtrer par titre ou contenu
   - **Liste des conversations** : Triées par date, favorites en premier
   - **Indicateurs** : 📌 favorite, ◈ agent actif, 📱 responsive
3. Cliquez sur une conversation pour la **charger**
4. Boutons d'action :
   - **📌** : Basculer en favori
   - **✕** : Supprimer la conversation

### Exemple de Suppression

#### Supprimer une Conversation
```javascript
window.deleteArchiveChat = async id => {
  if (!confirm("Supprimer cette conversation ?")) return;
  await db.delete('chats', id);
  if (state.chatId === id) await newChat();
  await renderArchives();
  toast("Conversation supprimée", "success");
};
```

**Action** :
1. Ouvrez les Archives
2. Survolez une conversation
3. Cliquez sur **✕**
4. Confirmation : "Supprimer cette conversation ?"
5. Toast : "Conversation supprimée"

#### Supprimer un Agent
```javascript
window.deleteAgent = async id => {
  if (!confirm("Supprimer cet agent ?")) return;
  await db.delete('agents', id);
  if (state.agent?.id === id) state.agent = null;
  await loadAgents();
  toast("Agent supprimé", "success");
};
```

#### Supprimer une Mémoire
```javascript
window.memoryDelete = async id => {
  await db.delete('global_memory', id);
  state.globalMemories = state.globalMemories.filter(m => m.id !== id);
  renderMemoryList();
};
```

**Action** :
1. Ouvrez le panneau Mémoire (⬡ en bas à droite)
2. Cliquez sur **✕** à côté d'une entrée
3. La mémoire est instantanément retirée

---

## 💾 Export et Import des Données

### Export Complet (Backup)

**Fonction** : Sauvegardez **toutes** vos données dans un fichier JSON

```javascript
async function exportData() {
  const chats = await db.getAll('chats') || [];
  const agents = await db.getAll('agents') || [];
  const mems = await db.getAll('global_memory') || [];
  const settings = await db.getAll('settings') || [];
  
  const payload = {
    version: "2.0",
    exported: new Date().toISOString(),
    source: "VOANH",
    data: { chats, agents, global_memory: mems, settings }
  };
  
  const blob = new Blob([JSON.stringify(payload, null, 2)], { type:"application/json" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url;
  a.download = `voanh-backup-${new Date().toISOString().slice(0,10)}.voanh.json`;
  a.click();
  URL.revokeObjectURL(url);
  
  toast("Données exportées avec succès !", "success");
}
```

**Utilisation** :
1. Ouvrez les **Archives** (📦 en bas à gauche)
2. Cliquez sur **⬇ EXPORTER** dans l'en-tête
3. Téléchargement automatique : `voanh-backup-2025-01-15.voanh.json`
4. Stockez ce fichier en sécurité (cloud, disque dur, clé USB)

**Contenu du fichier** :
```json
{
  "version": "2.0",
  "exported": "2025-01-15T10:30:00.000Z",
  "source": "VOANH",
  "data": {
    "chats": [...],      // Toutes vos conversations
    "agents": [...],     // Tous vos agents personnalisés
    "global_memory": [...], // Toute votre mémoire globale
    "settings": [...]    // Configurations (nom IA, objectifs, etc.)
  }
}
```

### Import Complet (Restore)

**Fonction** : Restaurez un backup précédemment exporté

```javascript
async function importData(file) {
  const text = await file.text();
  const payload = JSON.parse(text);
  const data = payload.data || payload;
  
  let count = 0;
  if (data.chats?.length) {
    for (const c of data.chats) { await db.put('chats', c); count++; }
  }
  if (data.agents?.length) {
    for (const a of data.agents) { await db.put('agents', a); count++; }
  }
  if (data.global_memory?.length) {
    for (const m of data.global_memory) { await db.put('global_memory', m); count++; }
  }
  
  await memory.getAll();
  await loadAgents();
  await renderArchives();
  
  toast(`${count} éléments importés avec succès !`, "success");
}
```

**Utilisation** :
1. Ouvrez les **Archives**
2. Cliquez sur **⬆ IMPORTER** dans l'en-tête
3. Sélectionnez un fichier `.voanh.json` ou `.json`
4. Validation automatique et import
5. Toast : "XX éléments importés avec succès !"
6. **Rafraîchissement** : Conversations, agents et mémoires réapparaissent instantanément

### Export/Import d'un Agent Individuel

**Exporter un agent** :
```javascript
window.exportAgent = async (id) => {
  const ag = await db.get('agents', id);
  const blob = new Blob([JSON.stringify(ag, null, 2)], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `agent-${ag.name.replace(/\s+/g,'-')}.json`;
  a.click();
  URL.revokeObjectURL(url);
  toast(`Agent "${ag.name}" exporté`, "success");
};
```

**Importer un agent** :
```javascript
inp.onchange = async (e) => {
  const file = e.target.files[0];
  const text = await file.text();
  const ag = JSON.parse(text);
  if (!ag.name || !ag.desc) throw new Error("Fichier agent invalide");
  ag.id = uuid(); 
  ag.created = now();
  await db.put('agents', ag);
  await loadAgents();
  toast(`Agent "${ag.name}" importé`, "success");
};
```

**Utilisation** :
1. Ouvrez la modale **⚙ AGENT**
2. Cliquez sur **⬆ IMPORTER UN AGENT**
3. Sélectionnez un fichier `agent-NomDeLAgent.json`
4. L'agent apparaît dans la liste, prêt à être activé

### Exemple Complet de Workflow Backup/Restore

**Scénario** : Vous changez d'ordinateur

1. **Sur l'ancien PC** :
   - Ouvrez VOANH AI
   - Archives → ⬇ EXPORTER
   - Récupérez `voanh-backup-2025-01-15.voanh.json`
   - Transférez-le (email, cloud, clé USB)

2. **Sur le nouveau PC** :
   - Ouvrez VOANH AI (nouvelle installation)
   - Configurez votre clé API Mistral
   - Archives → ⬆ IMPORTER
   - Sélectionnez le fichier backup
   - **Magic** : Toutes vos conversations, agents et mémoires réapparaissent !

---

## 🎨 Design & Expérience Utilisateur

### Thème Cyberpunk Futuriste

- **Palette de couleurs** : Void (#020509), Cyan néon (#00e5ff), Neon vert (#00ff9d), Plasma orange (#ff6b35)
- **Polices** : Orbitron (titres), Share Tech Mono (code), Exo 2 (texte)
- **Effets** : Scanlines, glow néon, HUD borders, gradients futuristes
- **Animations** : Messages qui glissent, typing indicator, pulses, transitions fluides

### Responsive Design

- **Desktop** : Header fixe, chat scrollable, panneaux latéraux (mémoire/archives)
- **Mobile** : Menus collapsibles, boutons enlargis, layout adapté
- **Breakpoints** : 768px (tablet), 480px (mobile)

### Accessibilité

- **Contrastes élevés** : Texte clair sur fond sombre
- **Tailles adaptables** : Polices lisibles, boutons larges
- **Feedback visuel** : Toasts colorés, status pills animées

---

## 🛠️ Personnalisation Avancée

### Modifier les Modèles

Dans le code, éditez le tableau `MODELS` :

```javascript
const MODELS = [
  { id:"mistral-large-2512", name:"🔥 Mistral Omega", badge:"🔥 Puissant", ... },
  // Ajoutez/supprimez/modifiez des modèles
];
```

### Changer le Thème

Modifiez les variables CSS dans `:root` :

```css
:root {
  --cyan: #00e5ff;        /* Couleur principale */
  --neon: #00ff9d;        /* Accents */
  --plasma: #ff6b35;      /* Highlights */
  --font-display: 'Orbitron', monospace;
  /* ... */
}
```

### Ajuster les Prompts Système

Éditez la fonction `buildSystemPrompt()` pour modifier le comportement par défaut de l'IA.

---

## 📝 Licence & Crédits

- **Développé par** : VOANH AI Team
- **Moteur IA** : Mistral AI (https://mistral.ai)
- **UI Framework** : Bootstrap 5.3
- **Fonts** : Google Fonts (Orbitron, Share Tech Mono, Exo 2)
- **Licence** : Usage personnel et commercial autorisé

---

## 🆘 Support & Documentation

- **Docs Mistral** : [docs.mistral.ai](https://docs.mistral.ai)
- **Console Mistral** : [console.mistral.ai](https://console.mistral.ai)
- **Issues & Features** : Ouvrez une issue sur le repository GitHub
- **Politique de sécurité** : [SECURITY.md](./SECURITY.md) — signalement de vulnérabilités et risques connus

---

## 🎯 Roadmap

- [ ] Support multimodal avancé (images, audio)
- [ ] Plugins/extensions système
- [ ] Synchronisation cloud optionnelle (chiffrée)
- [ ] Mode collaboration multi-utilisateurs
- [ ] Analytics locaux (stats d'usage, productivité)

---

**VOANH AI** — *Votre Intelligence Artificielle Personnelle, Évoluée, Locale et Gratuite.*

🚀 **Commencez maintenant** : Ouvrez `index.html`, configurez votre clé API Mistral, et laissez l'IA travailler pour vous !

---

## Roadmap DUNIA AI

### 1. Vision du projet

**DUNIA AI** est un assistant IA personnel, entièrement local, gratuit et sans serveur. Il repose sur un seul fichier `index.html` intégrant l'API Mistral AI, un système de mémoire persistante (IndexedDB), des agents spécialisés générés automatiquement, et une interface sobre et accessible.

L'objectif à terme est de fournir un outil personnel complet pour organiser ses idées, automatiser des tâches répétitives, analyser des documents, et maintenir un contexte de travail entre les sessions — sans dépendance externe, sans abonnement obligatoire, sans fuite de données.

---

### 2. Agents de base à créer

Ces cinq agents constituent le kit de démarrage recommandé pour couvrir les usages les plus courants :

| Agent | Rôle | Modèle conseillé |
|-------|------|-----------------|
| **Rédacteur Pro** | Rédaction de contenus clairs, reformulation, résumés | Mistral Zenith |
| **Analyste de données** | Lecture de CSV/JSON, interprétation de chiffres, synthèses | Mistral Omega |
| **Développeur assistant** | Code, débogage, revue de code, explication technique | Codestral / Devstral |
| **Chef de projet** | Structuration de tâches, priorisation, plans d'action | Mistral Zenith |
| **Assistant recherche** | Veille, synthèse de sources, extraction d'informations | Mistral Omega |

Pour créer ces agents : ouvrir la modale **⚙ Agents** → remplir le formulaire ou utiliser **✦ Générer + d'agents**.

---

### 3. Roadmap en 7 étapes

| Étape | Objectif | Critère de succès |
|-------|----------|-------------------|
| **1 — Socle fonctionnel** | Application stable, sans bug bloquant, labels en français | Tous les tests manuels passent sans erreur console |
| **2 — Kit agents de base** | Créer et valider les 5 agents de démarrage | Chaque agent répond de façon cohérente avec son rôle |
| **3 — Mémoire enrichie** | Utiliser la mémoire globale pour maintenir un contexte de projet | L'IA cite correctement des faits mémorisés entre sessions |
| **4 — Gestion de fichiers** | Attacher, analyser et résumer des fichiers (PDF, texte, image) | Un résumé pertinent est produit à partir d'un fichier joint |
| **5 — Export / Archivage** | Exporter conversations et agents, restaurer sur une autre machine | Le backup `.voanh.json` se réimporte sans perte de données |
| **6 — Personnalisation avancée** | Thèmes, prompts système adaptés à l'utilisateur | L'interface est personnalisée et les agents reflètent l'usage réel |
| **7 — Stabilisation & documentation** | README à jour, zéro erreur console, UX fluide | Revue complète de l'interface sur desktop et mobile |

---

### 4. Risques techniques

| Risque | Probabilité | Impact | Mitigation |
|--------|-------------|--------|------------|
| Quota Free Tier Mistral dépassé | Moyenne | Élevé | Surveiller `console.mistral.ai` ; basculer sur Mistral Small pour les tâches légères |
| Clé API exposée en hébergement public | Élevée si mal configuré | Critique | Usage local uniquement, ou proxy backend obligatoire en multi-utilisateur |
| Perte de données IndexedDB | Faible | Élevé | Export régulier via Archives → ⬇ Exporter |
| Régression après modification du code | Moyenne | Moyen | Tester les 5 fonctions clés après chaque modification (`sendMessage`, `loadChat`, `saveChat`, `renderMessages`, `loadAgents`) |
| Incompatibilité navigateur | Faible | Moyen | Tester sur Chrome et Firefox ; IndexedDB et `fetch` sont supportés universellement depuis 2020 |
| Injection XSS via contenu dynamique | Faible (mitigé) | Élevé | La fonction `escapeHtml()` est appliquée sur tous les contenus utilisateur affichés via `innerHTML` |

---

### 5. Prochaines actions

Actions concrètes à réaliser dans l'ordre de priorité :

1. **Créer les 5 agents de base** via la modale ⚙ Agents et les tester sur des cas réels
2. **Alimenter la mémoire globale** avec les informations clés de vos projets en cours
3. **Faire un premier export de sauvegarde** (Archives → ⬇ Exporter) et le stocker en lieu sûr
4. **Tester le chargement d'un fichier** (image ou PDF) et valider la réponse de l'IA
5. **Vérifier le rendu mobile** : ouvrir `index.html` sur un smartphone ou réduire la fenêtre à 375 px
6. **Personnaliser le nom et l'objectif de l'IA** via le wizard si ce n'est pas encore fait

---

### 6. Checklist de validation

Avant de considérer l'application comme prête pour un usage quotidien, valider chaque point :

#### Fonctionnement de base
- [ ] La clé API Mistral est saisie et le statut **En ligne** s'affiche
- [ ] Un message est envoyé et une réponse est reçue sans erreur console
- [ ] Le bouton Envoyer est désactivé pendant la génération (pas de doublon)

#### Agents
- [ ] Au moins un agent est créé et activé
- [ ] Le switch d'agent en cours de conversation fonctionne sans perte d'historique
- [ ] Un agent peut être exporté et réimporté

#### Archives
- [ ] Une conversation est sauvegardée automatiquement après le premier message
- [ ] Charger une archive depuis le panneau ferme bien le panneau
- [ ] Supprimer une conversation l'efface de la liste

#### Mémoire
- [ ] Un fait peut être ajouté manuellement à la mémoire globale
- [ ] L'IA cite un fait mémorisé dans une nouvelle conversation
- [ ] Une entrée de mémoire peut être supprimée

#### Export / Import
- [ ] L'export produit un fichier `.voanh.json` valide
- [ ] L'import restaure conversations, agents et mémoires

#### Interface
- [ ] L'interface s'affiche correctement sur mobile (< 480 px)
- [ ] Aucune erreur critique dans la console navigateur (`F12 → Console`)
- [ ] Les trois thèmes (Cyberpunk, Minuit, Clair) sont fonctionnels
