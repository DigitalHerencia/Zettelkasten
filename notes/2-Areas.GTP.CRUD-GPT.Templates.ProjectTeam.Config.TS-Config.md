---
id: jlu0znyrcglinvja4ttmef5
title: TS-Config
desc: ''
updated: 1742537259208
created: 1742537252578
---

**config_worker.ts** (Code Examples)  
```json
// tsconfig.json example
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "lib": ["DOM", "ESNext"],
    "jsx": "react-jsx",
    "strict": true,
    "moduleResolution": "node",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true
  },
  "include": ["app", "components", "lib"]
}
