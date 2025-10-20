# UI Generation Workflow - Méthode optimisée

Guide complet pour générer interfaces propres avec AI builders (V0, Bolt, Lovable) en minimisant crédits.

## Principe clé

**Séparer structure et design = économie + qualité**

1. Wireframes fonctionnels AVANT style
2. Charte graphique séparée
3. Fusion finale = résultat pro

---

## Étape 1: Contexte projet (ESSENTIEL)

**Avant toute génération, AI builder doit comprendre:**

- **Objectif projet**: Quel problème résout-il?
- **Utilisateurs**: Qui utilise l'app? (rôles, permissions)
- **Modèles données**: Quelles entités? (User, Listing, etc.)
- **Règles métier**: Validations, workflows critiques

**Pourquoi?** Sans contexte, AI génère composants génériques déconnectés du métier.


---

## Étape 2: Générer prompts wireframes

> **📋 Template réutilisable:** Consulte [ui-generation-prompt-template.md](./ui-generation-prompt-template.md) pour modèle complet avec exemples et variables à remplir.

**Action:** Lire attentivement chaque prompt généré avant d'aller sur V0.

---

## Étape 3: Générer wireframes sur V0

### Consignes critiques V0

**⚠️ INSISTER LOURDEMENT:**

> "Generate WIREFRAME ONLY. No colors, no branding, no custom styling. Use default shadcn/ui components with neutral gray palette. Focus on layout structure and functionality. I will apply design system later."

**Pourquoi c'est crucial:**
- Wireframe propre = structure solide
- Évite refonte complète si design change
- **Économie crédits**: 1 wireframe clean > 5 itérations design raté

**Process V0:**
**URL:** [v0.dev](https://v0.dev)

1. Nouveau projet V0
2. Coller prompt des écrans
3. **AJOUTER en préambule**: "WIREFRAME ONLY, default shadcn, no colors"
4. Générer
5. Vérifier structure layout/composants (ignorer couleurs)
6. Répéter pour chaque écran
7. **Itérer jusqu'à structure parfaite** (layout, spacing, responsive)

**Checklist wireframe validé:**
- [ ] Layout responsive (mobile/tablet/desktop)
- [ ] Composants fonctionnels (inputs, buttons, modals)
- [ ] Spacing cohérent (gaps, padding)
- [ ] Navigation logique
- [ ] États interactifs (hover, disabled, error)
- [ ] **Pas de couleurs custom** (gris neutres uniquement)

**Résultat:** Projet V0 avec wireframes propres, prêt pour charte graphique.

---

## Étape 4: Créer charte graphique

**Définir avant tweakcn:**

### Palette couleurs

**Méthode 1: Inspiration métier**
- BTM = ski, montagne → bleus froids, blancs neige, accents chaleureux
- Exemple: `#2563EB` (primary blue), `#F97316` (accent orange), `#64748B` (neutral)

**Méthode 2: Outils génération**
- [Coolors.co](https://coolors.co) - Générateur palettes
- [Adobe Color](https://color.adobe.com) - Harmonies couleurs
- [Realtime Colors](https://www.realtimecolors.com) - Preview live

**Output charte:**
```
Primary: #2563EB (bleu professionnel)
Secondary: #F97316 (orange montagne)
Neutral: #64748B (gris moderne)
Success: #10B981
Error: #EF4444
Background: #F8FAFC
Text: #0F172A
```

### Typographie

**Règles:**
- 1 font principale (titres + texte) OU 2 max (titres + body)
- Google Fonts recommandé (rapide, gratuit)

**Exemples professionnels:**
- Moderne: Inter, Outfit, Manrope
- Corporate: Roboto, Open Sans, Lato
- Élégant: Playfair Display, Merriweather

**Output charte:**
```
Primary font: Inter (headings + body)
OU
Heading font: Outfit (titres)
Body font: Inter (texte)
```

*Bonne ressource*: https://fontjoy.com/

---

## Étape 5: Générer thème sur tweakcn

**URL:** [tweakcn.com](https://tweakcn.com)

### Process tweakcn

1. Aller sur **tweakcn.com**
2. Cliquer onglet **"Generate"**
3. Remplir formulaire:
   - **Primary color**: `#2563EB`
   - **Secondary color**: `#F97316` (si applicable)
   - **Font family**: `Inter`
   - **Border radius**: `0.5rem` (ou selon préférence)
4. Cliquer **"Generate Theme"**
5. **Copier code généré** (CSS variables + Tailwind config)

**Code obtenu (exemple):**
```css
/* globals.css */
:root {
  --primary: 221 83% 53%;
  --secondary: 24 95% 53%;
  --background: 210 40% 98%;
  --foreground: 222 47% 11%;
  /* ... autres variables ... */
}
```

---

## Étape 6: Appliquer thème sur V0

### Process application

1. Sur V0, **dupliquer projet wireframe**
   - Nom: `[Projet] - With Design System`
2. Dans nouveau projet, ouvrir **Settings** ou fichier `globals.css`
3. **Remplacer variables CSS** par code tweakcn
6. **Prompt magique à V0:**

```
Apply the custom theme defined in globals.css```

7. Regénérer ou demander refresh
8. **Vérifier cohérence** sur tous écrans

**Résultat:** Wireframes + charte graphique appliquée = UI finale pro.

---

## Ressources

- **Google Fonts:** https://fonts.google.com
- **WCAG Contrast Checker:** https://webaim.org/resources/contrastchecker
- **V0 Docs:** https://v0.dev/docs
