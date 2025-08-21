# 🎯 Estimation de Trajectoire de Missile par Filtre de Kalman Étendu (EKF)

## 📌 Contexte et Objectifs Métier

La capacité à estimer précisément la trajectoire d’un objet mobile à partir de mesures bruitées est critique dans de nombreux domaines : défense, navigation autonome, radar, ou robotique.  
Ce projet vise à mettre en œuvre un **Filtre de Kalman Étendu (EKF)** pour l’estimation de la trajectoire d’un missile, à partir de mesures angulaires (azimut) simulées à partir de capteurs fixes.

Ce travail a été réalisé dans le cadre du cours de **Filtrage Linéaire et Non-Linéaire** à l’ENSAI, avec une forte composante mathématique et algorithmique.

---

## 👨‍💻 Ma Contribution

### 1. Démonstration mathématique du filtre EKF

Développement rigoureux des équations du filtre avec justification des étapes :

- **Initialisation** :
  ```math
  \hat{X}_0 = \frac{Y_0 \cdot \sigma^2}{\tau^2 + \sigma^2}, \quad P_0 = \frac{\sigma^2 \cdot \tau^2}{\tau^2 + \sigma^2}
  ```

- **Étape de prédiction** :
  ```math
  \hat{X}_n^- = a\hat{X}_{n-1}, \quad P_n^- = a^2P_{n-1} + \sigma^2
  ```

- **Mise à jour** :
  ```math
  \hat{X}_n = \hat{X}_n^- + \frac{P_n^-}{P_n^- + \tau^2}(Y_n - \hat{X}_n^-)
  ```

### 2. Simulation des données

Conception d’un simulateur réaliste de trajectoires basé sur le **modèle NCV** (Nearly Constant Velocity) avec bruit gaussien :

```r
X[,n] <- F %*% X[,n-1] + W[n,]
```

Génération de mesures bruitées à partir d’observations angulaires (capteur fixe) :

```r
theta <- atan((X[2,] - s1[2])/(X[1,] - s1[1])) + rnorm(T, sd=sigma_v)
```

## 🔧 Paramètres réalistes utilisés

- **Δ (pas de temps)** : 0.01 s  
- **σ (écart-type du bruit de mesure angulaire)** : 0.05 rad  
- **Modèle de mouvement** : Nearly Constant Velocity (NCV)  
- **Capteur** : station fixe simulant un capteur de mesure angulaire

Ces choix de paramètres permettent de reproduire un contexte opérationnel réaliste pour un système de suivi de missile ou de drone en environnement bruyant.

---

## 📈 Résultats

- Reconstitution précise de la trajectoire réelle à partir de données bruitées
- Estimation fiable de la position et de la vitesse à chaque instant
- Visualisation comparative entre trajectoire vraie, trajectoire mesurée (angle), et trajectoire estimée
- Confirmation de la stabilité du filtre face à différentes conditions de bruit

---

## 💼 Applications métier

Les filtres de Kalman étendus sont largement utilisés dans :

- 🛰️ **L'aéronautique et l’aérospatial** : guidage de trajectoire, navigation inertielle
- 🛡️ **La défense** : suivi de cibles, interception balistique
- 🚗 **La mobilité autonome** : estimation de position pour véhicules autonomes ou robots mobiles
- 📡 **Les télécommunications** : suivi de signaux mobiles et localisation en environnement urbain

Ce projet démontre la capacité d’un modèle EKF à fournir des estimations fiables et en temps réel à partir d’un flux de données partiellement observable et bruité.

---

## 👤 Auteur

**Sonokoli**  
Étudiant en 3e année à l’ENSAI – Spécialisation Data Science et Génie Statistique  
Projet encadré par **Salima El Kolei**, enseignante-chercheuse à l’ENSAI

---

## 📬 Contact

📧 sorobamara7@gmail.com
💼 [LinkedIn](https://www.linkedin.com/in/bamarasoro/)

---


