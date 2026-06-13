# 🇲🇱 Mali — Terre de Lumière

Site web statique professionnel sur le Mali, déployé sur Amazon S3 (AWS).

## 📁 Structure du projet

```
mali-site/
│
├── index.html          # Page principale
├── css/
│   └── style.css       # Styles (design system, animations, responsive)
├── js/
│   └── script.js       # Interactions, animations, compteurs
├── images/
│   ├── hero.jpg        # Image bannière hero
│   ├── djenné.jpg      # Mosquée de Djenné
│   ├── tombouctou.jpg  # Ville de Tombouctou
│   ├── dogon.jpg       # Pays Dogon / Falaises de Bandiagara
│   └── mali.jpg        # Carte / paysage du Mali
└── README.md
```

## 🎨 Design & Technologies

- **HTML5** — Structure sémantique (nav, section, article, footer)
- **CSS3** — Variables CSS, Grid, Flexbox, animations, responsive mobile-first
- **JavaScript (ES6+)** — IntersectionObserver, animations compteurs, effets parallaxe
- **Google Fonts** — Playfair Display + Inter + Cormorant Garamond
- Aucune dépendance externe (framework ou bibliothèque JS)

## 📄 Sections du site

1. **Hero** — Animation particules, titre animé, statistiques
2. **À propos** — Histoire du Mali, carte flottante
3. **Patrimoine UNESCO** — Djenné, Tombouctou, Pays Dogon
4. **Culture & Traditions** — Musique, artisanat, gastronomie...
5. **Chronologie** — Empires Ghana, Mali, Songhaï → Indépendance 1960
6. **Galerie** — Grille photo interactive avec effet parallaxe
7. **Contact** — Formulaire avec validation

## ☁️ Déploiement sur AWS S3

### Prérequis
- Compte AWS actif
- AWS CLI configuré (`aws configure`)

### Étapes de déploiement

```bash
# 1. Créer le bucket S3
aws s3 mb s3://mali-terre-de-lumiere --region eu-west-1

# 2. Activer l'hébergement web statique
aws s3 website s3://mali-terre-de-lumiere \
  --index-document index.html \
  --error-document index.html

# 3. Configurer la politique publique du bucket
aws s3api put-bucket-policy \
  --bucket mali-terre-de-lumiere \
  --policy file://bucket-policy.json

# 4. Uploader les fichiers
aws s3 sync . s3://mali-terre-de-lumiere \
  --exclude ".git/*" \
  --exclude "README.md" \
  --exclude "*.sh"

# 5. URL d'accès
# http://mali-terre-de-lumiere.s3-website-eu-west-1.amazonaws.com
```

### Fichier `bucket-policy.json`

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mali-terre-de-lumiere/*"
    }
  ]
}
```

## 🌐 URL du site (après déploiement)

```
http://<BUCKET_NAME>.s3-website-<REGION>.amazonaws.com
```

---

**Projet TP** — Cloud Computing · L3 Réseau Informatique  
**Auteur** — Arama Dev  
**Année** — 2025
