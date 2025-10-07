# ⚙️ Setup do Ambiente de Desenvolvimento — Metaflix

Bem-vindo ao ambiente de desenvolvimento do **Metaflix** 🎬
Este guia foi criado para garantir que **qualquer desenvolvedor interno** consiga subir o projeto localmente com facilidade, mantendo o mesmo padrão de ambiente utilizado pela equipe.

---

## 🧱 1. Pré-requisitos

Antes de iniciar, verifique se você possui as ferramentas corretas instaladas:

| Ferramenta             | Versão recomendada | Observação                                           |
| ---------------------- | ------------------ | ---------------------------------------------------- |
| **Node.js**            | ≥ 20.x             | Recomendado via [nvm](https://github.com/nvm-sh/nvm) |
| **pnpm**               | ≥ 9.x              | Gerenciador de pacotes utilizado pelo monorepo       |
| **Git**                | ≥ 2.40             | Para controle de versão e branches                   |
| **MongoDB**            | ≥ 6.x              | Banco de dados padrão do projeto                     |
| **Docker (opcional)**  | —                  | Usado apenas se preferir subir via container         |
| **VS Code (opcional)** | —                  | IDE recomendada com as extensões configuradas        |

---

## 🗂️ 2. Estrutura do projeto

O Metaflix utiliza **arquitetura limpa (Clean Architecture)** e um **monorepo** com **PNPM workspaces**.
Cada parte do sistema (frontend, backend, libs, SDKs, configs) está organizada para promover **reutilização, isolamento e escalabilidade**.

```
metaflix/
  apps/
    web/            # Aplicação principal (Next.js fullstack)
  packages/
    ui/             # Design system compartilhado
    types/          # Tipos e contratos globais
    services/       # SDKs, integrações e clients externos
    config/         # Configurações compartilhadas (eslint, tailwind, etc.)
  docs/             # Documentação do projeto
  tests/            # Testes e2e e contratos
  tools/            # Scripts e automações internas
```

📘 *Essa organização permite que múltiplos apps compartilhem os mesmos pacotes internos com consistência.*

---

## 🧩 3. Instalação e configuração inicial

### **Passo 1 — Clonar o repositório**

```bash
git clone https://github.com/sua-org/metaflix.git
cd metaflix
```

---

### **Passo 2 — Instalar dependências**

O projeto utiliza **pnpm** como gerenciador de pacotes.
Se ainda não tiver instalado:

```bash
npm install -g pnpm
```

Em seguida, rode:

```bash
pnpm install
```

Isso instalará **todas as dependências** de todos os workspaces automaticamente.

---

### **Passo 3 — Configurar variáveis de ambiente**

Cada app e pacote que precisa de variáveis de ambiente possui seu próprio arquivo `.env`.
Crie um arquivo `.env.local` dentro de `apps/web/` com base no modelo `.env.example`.

Exemplo:

```bash
cp apps/web/.env.example apps/web/.env.local
```

Edite os valores conforme seu ambiente local:

```env
# apps/web/.env.local
DATABASE_URL=mongodb://localhost:27017/metaflix
NEXTAUTH_SECRET=chave-secreta-dev
NEXT_PUBLIC_API_URL=http://localhost:3000/api
```

---

### **Passo 4 — Iniciar o servidor**

```bash
pnpm dev
```

Por padrão, o app web estará acessível em:

```
http://localhost:3000
```

---

### **Passo 5 — Banco de dados (MongoDB)**

Se você tiver o MongoDB instalado localmente, ele já deve rodar automaticamente.
Caso prefira usar via **Docker**, utilize:

```bash
docker run -d \
  --name metaflix-db \
  -p 27017:27017 \
  -v metaflix_data:/data/db \
  mongo:latest
```

---

## 🚀 4. Scripts disponíveis

Os principais scripts podem ser executados a partir da raiz do projeto (`metaflix/`):

| Comando        | Descrição                                    |
| -------------- | -------------------------------------------- |
| `pnpm dev`     | Inicia o ambiente de desenvolvimento local   |
| `pnpm build`   | Gera o build de produção                     |
| `pnpm lint`    | Executa o linter (ESLint)                    |
| `pnpm test`    | Roda os testes configurados                  |
| `pnpm format`  | Formata o código com Prettier                |
| `pnpm db:seed` | (Opcional) Popula o banco com dados iniciais |

💡 *Os scripts adicionais podem ser encontrados no `package.json` de cada pacote ou app.*

---

## 🧠 5. Dicas e boas práticas

* Use o comando `pnpm i nome-do-pacote -r` para instalar dependências em todos os workspaces.
* Utilize sempre **branches específicas por feature ou fix** (ex: `frontend/feature/payments-page`).
* Mantenha o padrão de commits semânticos:

  ```
  feat: adiciona tela de pagamentos
  fix: corrige erro no login
  refactor: melhora performance da busca
  ```
* Sempre atualize sua branch com `metaflix` antes de criar novas features.
* Documente alterações relevantes no `CHANGELOG.md` quando aplicável.

---

## 🧩 6. Estrutura lógica interna (resumo rápido)

| Diretório              | Finalidade                                                        |
| ---------------------- | ----------------------------------------------------------------- |
| **apps/web/app/**      | Páginas e rotas do Next.js                                        |
| **apps/web/core/**     | Lógica de domínio (entidades, casos de uso, portas e adaptadores) |
| **apps/web/lib/**      | Funções auxiliares, conexões e autenticação                       |
| **apps/web/infra/**    | Implementações concretas de banco, autenticação e gateways        |
| **packages/ui/**       | Componentes de interface reutilizáveis                            |
| **packages/types/**    | Tipagens e contratos de dados compartilhados                      |
| **packages/services/** | SDKs e integrações externas (ex: APIs, gateways)                  |
| **packages/config/**   | Configurações unificadas de lint, tailwind e tsconfig             |
| **docs/**              | Documentação técnica e guias internos                             |
| **tests/**             | Testes automatizados (E2E e unitários)                            |
| **tools/**             | Scripts internos e pipelines de automação                         |

---

## 🧾 7. Glossário de siglas e nomenclaturas técnicas

| Termo / Sigla          | Significado                       | Descrição                                                                     |
| ---------------------- | --------------------------------- | ----------------------------------------------------------------------------- |
| **API**                | Application Programming Interface | Interface de comunicação entre sistemas                                       |
| **DTO**                | Data Transfer Object              | Objeto para transferência segura de dados                                     |
| **UI**                 | User Interface                    | Camada de interface do usuário                                                |
| **SDK**                | Software Development Kit          | Conjunto de ferramentas para integração com serviços externos                 |
| **DB**                 | Database                          | Banco de dados                                                                |
| **Infra**              | Infrastructure                    | Camada de infraestrutura (implementações técnicas)                            |
| **Core**               | Núcleo                            | Camada de domínio e regras de negócio                                         |
| **Gateway**            | Adaptador de integração           | Interface entre o sistema e serviços externos                                 |
| **Entity**             | Entidade                          | Objeto principal de domínio (ex: Usuário, Pedido)                             |
| **Value Object**       | Objeto de valor                   | Representa valores imutáveis e comparáveis                                    |
| **Repo / Repository**  | Repositório                       | Camada que lida com persistência de dados                                     |
| **Clean Architecture** | —                                 | Arquitetura baseada em separação de responsabilidades e isolamento de camadas |
| **Monorepo**           | —                                 | Repositório único contendo múltiplos pacotes e apps                           |
| **PNPM Workspace**     | —                                 | Estrutura que gerencia múltiplos projetos com dependências compartilhadas     |

---

## 🧭 Conclusão

Com este setup, você está pronto para **rodar, entender e contribuir** com o projeto Metaflix com segurança.
A estrutura foi desenhada para ser **escalável, modular e fácil de manter**, respeitando boas práticas de desenvolvimento moderno e padrões de arquitetura limpa.

> 💡 *Dica final:* antes de iniciar qualquer desenvolvimento, confira se sua branch está atualizada com `metaflix` e execute `pnpm install` para garantir que tudo está sincronizado.


