# 🛡️ TP17 : Sécurité Kubernetes (RBAC, Pod Security, NetworkPolicy, Kyverno, Falco)

![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Security](https://img.shields.io/badge/Security-Defense_in_Depth-red?style=for-the-badge&logo=security&logoColor=white)
![Kyverno](https://img.shields.io/badge/Kyverno-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)

## 📝 Présentation du projet
Ce dépôt contient le travail réalisé lors du TP17. L'objectif est d'appliquer la **défense en profondeur** à une application Kubernetes volontairement mal configurée. Nous avons abordé :
1. **L'identité et les permissions** (RBAC).
2. **Le durcissement des Pods** (securityContext, Pod Security Standards).
3. **La segmentation réseau** (NetworkPolicy).
4. **Les règles d'admission** (Policy as Code avec Kyverno).
5. **La surveillance continue** (Trivy, Kubescape, Falco).

👉 **[📄 Cliquez ici pour télécharger le rapport complet (rapport_tp17.pdf)](rapport_tp17.pdf)**

## 📂 Structure du Dépôt
- 📁 `manifests/` : Les fichiers YAML de l'application (durcis).
- 📁 `policies/` : Les règles Kyverno (Audit et Enforce).
- 📁 `captures/` : Les preuves visuelles de validation du TP.
- 📄 `rapport_tp17.pdf` : Le rapport détaillé.

---

## 🚀 Validation des étapes (Livrables)

### 🟢 Partie 1 & 2 : RBAC et securityContext
**Vérification des permissions avec `kubectl auth can-i` :**
![RBAC Can I](captures/rbac-can-i.png)

---

### 🟢 Partie 3 : Pod Security Standards
**Refus de création d'un Pod privilégié par le profil `restricted` :**
![PSS Denied](captures/pss-denied.png)

---

### 🟢 Partie 4 : NetworkPolicies
**Test de la segmentation réseau (Frontend → API OK, Intrus → API en timeout) :**
![Network Policy](captures/netpol.png)

---

### 🟢 Partie 5 : Policy as Code avec Kyverno
**Refus d'un déploiement non conforme (mode Enforce) avec le message d'erreur :**
![Kyverno Enforce](captures/kyverno-enforce.png)

**Test des policies hors cluster avec la CLI Kyverno :**
![Kyverno CLI](captures/kyverno-cli.png)

---

### 🟢 Partie 6 : Analyse continue et détection
**Rapports Trivy Operator et score Kubescape :**
![Trivy Kubescape](captures/trivy-kubescape.png)

**Alerte de sécurité générée par Falco après une action suspecte :**
![Falco Alert](captures/falco-alert.png)

---

## 🔒 Sécurité et Bonnes Pratiques
- Utilisation de `automountServiceAccountToken: false` pour limiter les accès.
- Application du principe du moindre privilège (RBAC).
- Utilisation de `runAsNonRoot` et `readOnlyRootFilesystem`.
- Aucune image avec le tag `latest` n'est autorisée en production.
