# InfinityTalk

Application de communication collaborative - Monorepo avec NestJS (API) et Next.js (Web)

## Structure du Projet

```
InfinityTalk/
├── apps/
│   ├── api/          # NestJS Web API (Backend)
│   └── web/          # Next.js Frontend
├── shared/           # Code partagé (types, utils)
└── diagrams/         # Diagrammes du projet
```

## Technologies

- **Backend**: NestJS (TypeScript)
- **Frontend**: Next.js (TypeScript, React)
- **Shared**: TypeScript

## Scripts

- `npm run dev:api` - Démarrer l'API en mode développement
- `npm run dev:web` - Démarrer le frontend en mode développement
- `npm run build` - Build tous les projets
