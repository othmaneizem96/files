# 🎯 RecrutAI — Déploiement sur Render.com

## Structure des fichiers

```
recrut_ai/
├── app.py                  ← Serveur Flask
├── analyzer.py             ← Logique d'analyse
├── templates/
│   └── index.html          ← Interface web
├── requirements.txt        ← Dépendances (+ gunicorn)
├── render.yaml             ← Config déploiement Render
└── README.md
```

---

## 🚀 Déploiement sur Render.com (GRATUIT)

### Pourquoi Render et pas Netlify ?
Netlify n'héberge que des sites statiques. Render supporte Python/Flask nativement.

### Étape 1 — GitHub

1. Créez un compte sur **github.com**
2. Créez un nouveau dépôt (ex: `recrut-ai`)
3. Uploadez tous les fichiers du projet

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/VOTRE_NOM/recrut-ai.git
git push -u origin main
```

### Étape 2 — Render

1. Créez un compte sur **render.com**
2. Cliquez **New → Web Service**
3. Connectez votre dépôt GitHub
4. Render détecte automatiquement `render.yaml`

### Étape 3 — Clé API cachée ⭐

Dans le dashboard Render → votre service → **Environment** :

| Key | Value |
|-----|-------|
| `RESUMEPARSER_API_KEY` | `votre_cle_api_ici` |

✅ La clé est **invisible** pour les utilisateurs — elle ne passe jamais dans le navigateur.

### Étape 4 — Déployer

Cliquez **Deploy** → votre app sera disponible sur :
`https://recrut-ai.onrender.com`

---

## 🔒 Sécurité — ce qui est protégé

| Information | Visible par l'utilisateur ? |
|-------------|----------------------------|
| Clé API resumeparser.app | ❌ Non — côté serveur uniquement |
| Solde de crédits API | ❌ Non — supprimé des réponses |
| Fichiers CV des autres sessions | ❌ Non — isolés par session ID |
| Fichiers supprimés après analyse | ✅ Oui — nettoyage automatique |

---

## 💻 Lancement local (avec clé cachée)

```bash
# Windows
set RESUMEPARSER_API_KEY=votre_cle
python app.py

# Mac / Linux
RESUMEPARSER_API_KEY=votre_cle python app.py
```

---

## ⚙️ Variables d'environnement

| Variable | Description | Obligatoire |
|----------|-------------|-------------|
| `RESUMEPARSER_API_KEY` | Clé API resumeparser.app | ✅ Oui |
| `SECRET_KEY` | Clé secrète Flask (auto sur Render) | Non |
| `FLASK_ENV` | `production` pour désactiver le debug | Non |
| `PORT` | Port (auto sur Render) | Non |
