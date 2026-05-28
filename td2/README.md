# PolyQuiz – Plateforme Interactive de Quiz

> Projet réalisé dans le cadre du TP Évalué n°2 – Ingénierie Front-End Avancée  
> École Nationale Supérieure Polytechnique de Maroua – Année 2025-2026  
> Enseignant : MANAODA DEUHWE Yves Hermann

---

## Description

**PolyQuiz** est une SPA React proposant des quiz chronométrés sur la F1, le MotoGP, la NBA et les Manga/Anime. Elle met en œuvre des patterns d'ingénierie avancés : Custom Hooks, Context API, Protected Routes, useReducer, useRef et useMemo.

---

## Jalons implémentés

| Jalon | Description | Points |
|-------|-------------|--------|
| 1 | `useFetch(url)` – Custom Hook réseau + `questions.json` | 3 pts |
| 2 | `UserContext` + `UserProvider` – API Context globale | 4 pts |
| 3 | `ProtectedRoute` – Sécurisation des routes `/quiz` et `/resultats` | 4 pts |
| 4 | `quizReducer` + `useReducer` – Machine à état complexe | 5 pts |
| 5 | `useRef` (chronomètre sans fuite mémoire) + `useMemo` (ratio) | 4 pts |

**Total visé : 20/20**

---

## Installation

```bash
npm install
```

## Lancement du serveur de développement

```bash
npm run dev
```

Application disponible sur [http://localhost:5173](http://localhost:5173)

## Build de production

```bash
npm run build
```

---

## Structure du projet

```
src/
├── components/
│   └── ProtectedRoute.jsx   # Jalon 3 : Garde de route (Context + Navigate)
├── context/
│   └── UserContext.jsx      # Jalon 2 : createContext + UserProvider + useUser
├── hooks/
│   ├── useFetch.js          # Jalon 1 : Custom Hook réseau (data/loading/error)
│   └── quizReducer.js       # Jalon 4 : Reducer (START/ANSWER/FINISH)
├── layouts/
│   └── Navbar.jsx           # Barre de navigation globale
├── pages/
│   ├── Accueil.jsx          # Page "/" : saisie du pseudo
│   ├── QuizEngine.jsx       # Page "/quiz" : moteur du quiz
│   └── Resultats.jsx        # Page "/resultats" : score + useMemo
├── App.jsx                  # Jalons 2 & 3 : Provider + BrowserRouter + Routes
└── main.jsx                 # Point d'entrée React
public/
└── questions.json           # Jalon 1 : 10 questions (F1, MotoGP, NBA, Manga)
```

---

## Patterns d'ingénierie implémentés

- **Custom Hook** : `useFetch` isole la logique réseau des composants graphiques
- **Context API** : `UserContext` élimine le Props Drilling pour pseudo & score
- **Protected Routes** : `ProtectedRoute` utilise `useContext` + `<Navigate>` de React Router
- **useReducer** : `quizReducer` gère START_QUIZ, ANSWER_QUESTION, FINISH_QUIZ
- **useRef** : stocke l'id du `setInterval` sans provoquer de re-rendus
- **useMemo** : protège le calcul du ratio contre les re-rendus inutiles (toggle thème)
- **Cleanup** : `clearInterval` dans le return de `useEffect` → zéro fuite mémoire
