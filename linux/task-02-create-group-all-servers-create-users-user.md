# Task 2 — Group Creation and User Assignment (Linux User Management)

**Context:** These tasks are part of a hands-on simulation on KodeKloud Engineer, where I act as a sysadmin for a fictional company (xFusionCorp Industries / Nautilus). The servers are real remote machines (accessed via SSH), and the tasks mirror real-world day-to-day sysadmin work — not just theory.

**Scenario:** xFusionCorp Industries — the system admin team has streamlined access management by implementing group-based access control.

**Goal:**
a. Create a group named `nautilus_developers` across all App Servers within the Stratos Datacenter.
b. Add the user `rajesh` to the `nautilus_developers` group on all App Servers. If the user doesn't exist, create it as well.

## What I did

1. Connected via SSH to each of the 3 Application Servers, using the credentials from the infrastructure documentation:
   ```
   ssh tony@stapp01
   ssh steve@stapp02
   ssh banner@stapp03
   ```
2. Checked that `rajesh` didn't exist yet (`id rajesh` → "no such user").
3. Created the group on each server:
   ```
   sudo groupadd nautilus_developers
   ```
4. Confirmed the group was created:
   ```
   getent group nautilus_developers
   ```
   or
   ```
   grep nautilus_developers /etc/group
   ```
5. Created the user `rajesh` already assigned to the group as a secondary group (`-G`, not `-g`, since he still gets his own primary group automatically):
   ```
   sudo useradd -G nautilus_developers rajesh
   ```
6. Confirmed with `id rajesh`:
   ```
   uid=1001(rajesh) gid=1002(rajesh) groups=1002(rajesh),1001(nautilus_developers)
   ```
7. Repeated steps 3–6 on all 3 servers.

## Mistakes and lessons along the way

- Confused `-g` (primary group) with `-G` (secondary group) at first — `-g` replaces the automatic primary group, `-G` adds without removing anything.
- Typed `nautilus_developer` (missing the "s") when checking the group. `grep` still matched because it searches for partial text, but `getent group` found nothing because it requires an exact name match — that difference confused me for a bit until I compared both commands side by side.
- Didn't know the account-verification commands (`getent group` / `grep /etc/group`) yet, since I'd only used `id` for users before, not groups.

---

# Task 2 — Criação de Grupo e Atribuição de Usuário (Gerenciamento de Usuários Linux)

**Contexto:** Essas tarefas fazem parte de uma simulação prática na plataforma KodeKloud Engineer, onde atuo como sysadmin de uma empresa fictícia (xFusionCorp Industries / Nautilus). Os servidores são máquinas remotas reais (acessadas via SSH), e as tarefas reproduzem o dia a dia real de um sysadmin — não é só teoria.

**Cenário:** xFusionCorp Industries — o time de administração de sistemas simplificou o gerenciamento de acesso implementando controle de acesso baseado em grupo.

**Objetivo:**
a. Criar um grupo chamado `nautilus_developers` em todos os App Servers do Stratos Datacenter.
b. Adicionar o usuário `rajesh` ao grupo `nautilus_developers` em todos os App Servers. Se o usuário não existir, criá-lo também.

## O que eu fiz

1. Conectei via SSH em cada um dos 3 Application Servers, usando as credenciais da documentação de infraestrutura:
   ```
   ssh tony@stapp01
   ssh steve@stapp02
   ssh banner@stapp03
   ```
2. Confirmei que o `rajesh` ainda não existia (`id rajesh` → "no such user").
3. Criei o grupo em cada servidor:
   ```
   sudo groupadd nautilus_developers
   ```
4. Confirmei que o grupo foi criado:
   ```
   getent group nautilus_developers
   ```
   ou
   ```
   grep nautilus_developers /etc/group
   ```
5. Criei o usuário `rajesh` já atribuído ao grupo como secundário (`-G`, não `-g`, já que ele continua recebendo o próprio grupo primário automaticamente):
   ```
   sudo useradd -G nautilus_developers rajesh
   ```
6. Confirmei com `id rajesh`:
   ```
   uid=1001(rajesh) gid=1002(rajesh) groups=1002(rajesh),1001(nautilus_developers)
   ```
7. Repeti os passos 3–6 nos 3 servidores.

## Erros e aprendizados no caminho

- Confundi `-g` (grupo primário) com `-G` (grupo secundário) no início — `-g` substitui o grupo primário automático, `-G` adiciona sem remover nada.
- Digitei `nautilus_developer` (sem o "s") ao consultar o grupo. O `grep` mesmo assim encontrou porque busca por texto parcial, mas o `getent group` não retornou nada porque exige o nome exato — essa diferença me confundiu até eu comparar os dois comandos lado a lado.
- Ainda não conhecia os comandos de verificação de grupo (`getent group` / `grep /etc/group`), já que antes só tinha usado `id` para usuários, não para grupos.
