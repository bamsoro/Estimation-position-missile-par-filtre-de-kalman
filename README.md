# Estimation de Trajectoire de Missile par Filtre de Kalman Étendu

![Visualisation des trajectoires](results/trajectory_comparison.png)

## 📌 Présentation du Projet
Implémentation d'un filtre de Kalman étendu (EKF) pour estimer la trajectoire d'un missile à partir de mesures angulaires bruitées. Développé dans le cadre du cours de Filtrage Linéaire et Non-Linéaire à l'ENSAI.

## 👨‍💻 Ma Contribution

### 1. Démontration Mathématique du Filtre
J'ai établi les fondements théoriques du filtre en démontrant :

**Initialisation :**
```math
\hat{X}_0 = \frac{Y_0 \cdot \sigma^2}{\tau^2 + \sigma^2}, \quad P_0 = \frac{\sigma^2 \cdot \tau^2}{\tau^2 + \sigma^2}
```

**Étape de Prédiction :**

```math
\hat{X}_n^- = a\hat{X}_{n-1}, \quad P_n^- = a^2P_{n-1} + \sigma^2
```


**Mise à Jour :**

```math
\hat{X}_n = \hat{X}_n^- + \frac{P_n^-}{P_n^- + \tau^2}(Y_n - \hat{X}_n^-)
```


### 2. Simulation des Données
J'ai implémenté le simulateur complet comprenant :

- Modèle NCV (Nearly Constant Velocity) avec bruits gaussiens
```r
X[,n] <- F %*% X[,n-1] + W[n,]
```

**Génération des mesures bruitées**

```r
theta <- atan((X[2,] - s1[2])/(X[1,] - s1[1])) + rnorm(T, sd=sigma_v)
```

**Configuration des paramètres réalistes (Δ=0.01s, σ=0.05 rad)**

## 🛠️ Implémentation Technique

### Modèle Mathématique
```math
\begin{aligned}
&\text{Modèle d'état :} \\
&\mathbf{X}_n = \mathbf{F}\mathbf{X}_{n-1} + \mathbf{W}_n \\
&\text{avec } \mathbf{F} = \begin{pmatrix}
1 & 0 & Δ & 0 \\
0 & 1 & 0 & Δ \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}, \quad \mathbf{W}_n \sim \mathcal{N}(0,\mathbf{Q})
\end{aligned}
```

```math
\begin{aligned}
&\text{Modèle de mesure :} \\
&\theta_n = \tan^{-1}\left(\frac{Z_n-s_z}{X_n-s_x}\right) + V_n, \quad V_n \sim \mathcal{N}(0,\tau^2)
\end{aligned}
```


## 👤 Auteur

**Sonokoli**  
Étudiant en 3e année à l’ENSAI – Spécialisation Data Science et génie statistiques
Projet réalisé sous la supervision de Youssef Esstafa

---

## 📬 Contact

Pour toute question ou suggestion :  
📧 [sorobamara7@gmail.com]
