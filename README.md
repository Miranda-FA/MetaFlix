# 🎬 Metaflix

Bem-vindo ao repositório **Metaflix**!  

Este é um **monorepo fullstack moderno**, organizado para ser **escalável, reutilizável e fácil de manter**. Ele combina **frontend, backend e pacotes compartilhados**, seguindo **Clean/Hexagonal Architecture**.

---

## 🏗️ Nossa Arquitetura Visual

A arquitetura do Metaflix protege a **lógica de negócio** e separa claramente **domínio, aplicação e infraestrutura**.  

```

```
      ┌───────────────────────────┐
      │        🌐 Frontend         │
      │ apps/web (Next.js)        │
      │ UI, Pages, Components     │
      └─────────────┬─────────────┘
                    │
                    ▼
      ┌───────────────────────────┐
      │      📦 Application / UI   │
      │ components/ui + domain    │
      │ app/routes / pages        │
      └─────────────┬─────────────┘
                    │
                    ▼
      ┌───────────────────────────┐
      │ ❤️ Core (Domínio)         │
      │ core/domain + core/application │
      │ Entities, Value Objects,  │
      │ Use-Cases, Services       │
      └─────────────┬─────────────┘
                    │
                    ▼
      ┌───────────────────────────┐
      │ 🔌 Ports & Adapters        │
      │ Repositories | Gateways   │
      │ Interfaces do domínio     │
      └─────────────┬─────────────┘
                    │
                    ▼
      ┌───────────────────────────┐
      │ 🛠️ Infraestrutura           │
      │ infra/db, infra/auth,     │
      │ infra/external            │
      │ Banco, Auth, Integrações  │
      └───────────────────────────┘
```

```

💡 **Analogia:**  
O **Core** é o coração da aplicação. Infraestrutura e Frontend são órgãos e músculos que conectam o coração ao mundo. Se o coração estiver forte, todo o corpo funciona perfeitamente.

---

## 🌳 Estrutura de Pastas

```

metaflix/
├─ apps/          # Aplicações principais
│   └─ web/       # Next.js fullstack
│       ├─ app/           # Rotas, páginas e layouts
│       ├─ components/    # UI e componentes de domínio
│       ├─ lib/           # Helpers: db, auth, validators
│       ├─ core/          # Domínio e casos de uso
│       ├─ infra/         # Implementações concretas
│       ├─ middleware.ts  # Middlewares
│       └─ package.json
├─ packages/      # Pacotes compartilhados (UI, types, services, config)
├─ docs/          # Documentação
├─ tests/         # Testes E2E e de contratos
├─ tools/         # Scripts auxiliares
├─ turbo.json     # Configuração TurboRepo
├─ package.json   # Dependências globais
└─ pnpm-workspace.yaml # Workspaces PNPM

```

---

## ⚡ Fluxo de Branches & Convenções

```

main        ← branch de produção
metaflix    ← branch de desenvolvimento integrando features

````

| Tipo      | Source    | Merge em        | Exemplo de Nome                   |
|-----------|-----------|----------------|----------------------------------|
| feature   | metaflix  | metaflix       | frontend/feature/payment-dashboard |
| fix       | metaflix  | metaflix       | backend/fix/order-validation      |
| refactor  | metaflix  | metaflix       | frontend/refactor/ui-components   |
| hotfix    | main      | main → metaflix | backend/hotfix/cache-issue       |
| chore     | metaflix  | metaflix       | frontend/chore/update-deps       |
| docs      | metaflix  | metaflix       | backend/docs/update-api-docs     |
| test      | metaflix  | metaflix       | test/api-contracts               |

💡 **Dicas:**
- Sempre use o padrão `<área>/<tipo>/<assunto>`.  
- Crie branches apenas quando houver demanda real.  
- Nunca commit direto em `main` ou `metaflix`.

---

## 🚀 Como rodar localmente

```
# Instalar dependências
pnpm install

# Configurar variáveis de ambiente
MONGO_URI=mongodb://localhost:27017/metaflix
JWT_SECRET=supersecretkey

# Rodar a aplicação web
pnpm dev --filter apps/web
````

Abra [http://localhost:3000](http://localhost:3000) no navegador.

---

## 📚 Índice de Siglas e Termos Técnicos

| Sigla / Termo   | Significado                                                           |
| --------------- | --------------------------------------------------------------------- |
| DTO             | Data Transfer Object (objeto de transferência de dados entre camadas) |
| E2E             | End-to-End (testes que simulam fluxo completo)                        |
| API             | Application Programming Interface                                     |
| SDK             | Software Development Kit                                              |
| PNPM            | Gerenciador de pacotes para monorepos                                 |
| TurboRepo       | Otimiza builds, testes e cache em monorepos                           |
| Clean/Hexagonal | Arquitetura que separa domínio, aplicação e infraestrutura            |
| Repository      | Classe ou interface que gerencia persistência de dados                |
| Gateway         | Interface que comunica com serviços externos                          |
| Middleware      | Função intermediária entre requisição e resposta                      |
| Value Object    | Objeto que representa um valor imutável e validado                    |

---

## 🌟 Por que essa arquitetura?

* 💪 **Código desacoplado:** mudanças em infraestrutura ou frontend não quebram a lógica de negócio.
* 🧪 **Testabilidade:** Core testável sem depender de banco ou UI.
* 🚀 **Escalabilidade:** novos módulos e apps podem ser adicionados sem bagunçar a estrutura.
* ♻️ **Reutilização:** serviços, tipos e componentes compartilháveis entre apps.
* 🧭 **Organização clara:** onboarding de novos desenvolvedores rápido e intuitivo.

---

## 🎯 Objetivos do Metaflix

* Criar um sistema **limpo, escalável e sustentável**
* Garantir **reutilização e consistência**
* Facilitar **desenvolvimento seguro e rastreável**
* Fornecer **documentação clara e didática** para todos os colaboradores

---
