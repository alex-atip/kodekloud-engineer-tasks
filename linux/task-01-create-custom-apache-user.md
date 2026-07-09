# Task 1 — Create Custom Apache User (Linux User Management)

**Context:** These tasks are part of a hands-on simulation on KodeKloud Engineer, where I act as a sysadmin for a fictional company (xFusionCorp Industries / Nautilus). The servers are real remote machines (accessed via SSH), and the tasks mirror real-world day-to-day sysadmin work — not just theory.

**Scenario:** xFusionCorp Industries / Stratos Datacenter — working as user `tony` (sysadmin) on Application Server 1.

**Goal:** Create a new system user (`mariyam`) with a specific UID, on a different server on the network.

## What I did

1. Switched servers via SSH, using their documentation to find the hostname and credentials.
   ```
   ssh usuario@hostname
   ```
2. Looked up the `useradd` command in KodeKloud's notes to remember the correct flags.
3. Final working command:
   ```
   sudo useradd -u 1785 -d /var/www/mariyam mariyam
   ```
4. Confirmed with `id mariyam`:
   ```
   uid=1785(mariyam) gid=1785(mariyam) groups=1785(mariyam)
   ```

## Mistakes and lessons along the way

- Switching servers was new to me — had to understand the logic of accessing another server via SSH using their docs.
- Didn't remember how to add a user; researched the docs to learn how to look it up anywhere, and that's how I recalled the flags.
- Confused the UID concept with "permissions" (like a GUID) — UID is just a unique identifier, not what controls access.
- Mistyped the sudo password for tony several times, confusing special characters (0 with O).
- Forgot to put the username at the end of the `useradd` command.
- Didn't remember how to check if the user was created — it's just `id nome_do_usuario`.

---

# Task 1 — Criar Usuário Apache Customizado (Gerenciamento de Usuários Linux)

**Contexto:** Essas tarefas fazem parte de uma simulação prática na plataforma KodeKloud Engineer, onde atuo como sysadmin de uma empresa fictícia (xFusionCorp Industries / Nautilus). Os servidores são máquinas remotas reais (acessadas via SSH), e as tarefas reproduzem o dia a dia real de um sysadmin — não é só teoria.

**Cenário:** xFusionCorp Industries / Stratos Datacenter — trabalhando como o usuário `tony` (sysadmin) no Application Server 1.

**Objetivo:** Criar uma nova usuária no sistema (`mariyam`) com um UID específico, em outro servidor da rede.

## O que eu fiz

1. Troquei de servidor via SSH, usando a documentação deles para entender o nome do host e as credenciais.
   ```
   ssh usuario@hostname
   ```
2. Pesquisei o comando `useradd` nas notes do KodeKloud para relembrar as flags corretas.
3. Comando final que funcionou:
   ```
   sudo useradd -u 1785 -d /var/www/mariyam mariyam
   ```
4. Confirmei com `id mariyam`:
   ```
   uid=1785(mariyam) gid=1785(mariyam) groups=1785(mariyam)
   ```

## Erros e aprendizados no caminho

- Troca de servidor era novo pra mim — precisei entender a lógica de acessar outro servidor via SSH usando a documentação deles.
- Não lembrava como adicionar usuário; pesquisei na documentação para aprender a consultar em qualquer lugar, e assim relembrei as flags.
- Confundi o conceito de UID com "permissões" (tipo GUID) — UID é só um identificador único do usuário, não controla acesso.
- Errei a senha do sudo do tony várias vezes por confundir caracteres especiais (0 com O).
- Esqueci de colocar o nome do usuário no final do comando `useradd`.
- Não lembrava como consultar se o usuário foi criado — era só `id nome_do_usuario`.
