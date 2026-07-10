# Task 03 - Creating a User with a Non-Interactive Shell

## Context
This task is part of a hands-on simulation for xFusionCorp Industries, a fictional company used by KodeKloud Engineer to practice real sysadmin scenarios on real Linux servers accessed via SSH.

## Scenario
The system admin team at xFusionCorp Industries needs to accommodate a backup agent tool's requirements. Part of the setup involves creating a user account that should never be able to open an interactive shell session.

## Goal
Create a user named `javed` with a non-interactive shell on App Server 3 (`stapp03`).

## What I did
1. Connected to the target server: `ssh banner@stapp03`
2. Checked which shells the system considers valid: `cat /etc/shells`
3. Instead of assuming the path from memory, looked up the actual location of the `nologin` binary on this system: `which nologin` -> `/usr/sbin/nologin`
4. Created the user with the non-interactive shell: `sudo useradd -s /usr/sbin/nologin javed`
5. Confirmed the user was created correctly: `id javed` -> `uid=1001(javed) gid=1001(javed) groups=1001(javed)`
6. Validated that the shell truly blocks interactive login by attempting: `su - javed` -> `su: Authentication failure` (expected behavior for a `nologin` shell)

## Mistakes and lessons along the way
- Initially considered adding the `-r` flag (system/reserved account), based on a similar task from a previous course. Re-read the task requirements and confirmed nothing indicated a system account was needed, so left `-r` out - only the non-interactive shell (`-s`) was required.
- Remembered the `nologin` path as `/usr/bin/nologin` from a previous course, but this system (Red Hat-based) actually had it at `/usr/sbin/nologin`. Used `which nologin` to confirm the real path instead of assuming it would be the same across distros - a good reminder that binary paths can vary between systems.
- Learned two different ways to validate a non-interactive shell without needing a full login attempt: `getent passwd javed` (checks the shell field directly) or `su - javed` (real login attempt, which should fail with "Authentication failure" rather than actually granting access).

---

# Task 03 - Criando um Usuário com Shell Não-Interativo

## Contexto
Esta task faz parte de uma simulação prática para a xFusionCorp Industries, uma empresa fictícia usada pelo KodeKloud Engineer para praticar cenários reais de administração de sistemas em servidores Linux reais, acessados via SSH.

## Cenário
A equipe de administração de sistemas da xFusionCorp Industries precisa atender aos requisitos de uma ferramenta de backup. Parte da configuração envolve criar uma conta de usuário que nunca deve conseguir abrir uma sessão de shell interativa.

## Objetivo
Criar um usuário chamado `javed` com shell não-interativo no App Server 3 (`stapp03`).

## O que eu fiz
1. Conectei no servidor alvo: `ssh banner@stapp03`
2. Verifiquei quais shells o sistema considera válidos: `cat /etc/shells`
3. Em vez de assumir o caminho de memória, consultei onde o binário `nologin` realmente está nesse sistema: `which nologin` -> `/usr/sbin/nologin`
4. Criei o usuário com o shell não-interativo: `sudo useradd -s /usr/sbin/nologin javed`
5. Confirmei que o usuário foi criado corretamente: `id javed` -> `uid=1001(javed) gid=1001(javed) groups=1001(javed)`
6. Validei que o shell realmente bloqueia login interativo tentando: `su - javed` -> `su: Authentication failure` (comportamento esperado para um shell `nologin`)

## Erros e aprendizados no caminho
- No início considerei usar a flag `-r` (conta de sistema/reservada), baseado numa task parecida de um curso anterior. Reli o enunciado e confirmei que nada indicava a necessidade de conta de sistema, então deixei o `-r` de fora — só o shell não-interativo (`-s`) era necessário.
- Lembrava o caminho do `nologin` como `/usr/bin/nologin` de um curso anterior, mas nesse sistema (baseado em Red Hat) ele na verdade estava em `/usr/sbin/nologin`. Usei `which nologin` pra confirmar o caminho real em vez de assumir que seria igual entre distros diferentes — um bom lembrete de que caminhos de binário podem variar entre sistemas.
- Aprendi duas formas diferentes de validar um shell não-interativo sem precisar de uma tentativa de login completa: `getent passwd javed` (confere o campo do shell diretamente) ou `su - javed` (tentativa real de login, que deve falhar com "Authentication failure" em vez de conceder acesso de fato).
