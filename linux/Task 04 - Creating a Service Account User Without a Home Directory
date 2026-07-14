# Task 04 - Creating a Service Account User Without a Home Directory

## Context
This task is part of a hands-on simulation for xFusionCorp Industries, a fictional company used by KodeKloud Engineer to practice real sysadmin scenarios on real Linux servers accessed via SSH.

## Scenario
In response to the latest tool implementation at xFusionCorp Industries, the system admins require the creation of a service user account. Service accounts are meant to run processes, not to be used for interactive logins, so they typically don't need a home directory.

## Goal
Create a user named `rose` on App Server 1 (`stapp01`) without a home directory.

## What I did
1. Connected to the target server: `ssh tony@stapp01`
2. The `-M` flag wasn't listed in the course's User Management documentation, so instead of guessing, ran `useradd --help` to check all available options on this system and located `-M, --no-create-home`
3. First attempt without elevated privileges: `useradd -M rose` -> `Permission denied` / `cannot lock /etc/passwd; try again later`
4. Re-ran with `sudo`: `sudo useradd -M rose` -> succeeded
5. Validated the user was created: `id rose` -> `uid=1001(rose) gid=1001(rose) groups=1001(rose)`
6. Checked the registered home path in `/etc/passwd`: `grep rose /etc/passwd` -> `rose:x:1001:1001::/home/rose:/bin/bash`
7. Confirmed the home directory doesn't actually exist on disk: `ls /home/` -> only `tony` was listed, `rose` was absent

## Mistakes and lessons along the way
- Forgot `sudo` on the first attempt, which failed with a permission error — a reminder that `useradd` always needs elevated privileges.
- The `-M` flag isn't covered in the course's User Management guide (which only lists the most common options). Confirmed it's a legitimate flag by checking `useradd --help` directly on the system, instead of assuming it didn't exist just because it wasn't in the doc.
- Learned that `-M` only stops the physical folder from being created — the home path still gets registered in `/etc/passwd` (e.g. `/home/rose`) even though the directory itself never exists on disk. Checking `/etc/passwd` alone isn't enough to confirm; `ls /home/` is needed to verify the folder truly wasn't created.

---

# Task 04 - Criando um Usuário de Conta de Serviço Sem Diretório Home

## Contexto
Esta task faz parte de uma simulação prática para a xFusionCorp Industries, uma empresa fictícia usada pelo KodeKloud Engineer para praticar cenários reais de administração de sistemas em servidores Linux reais, acessados via SSH.

## Cenário
Em resposta à mais recente implementação de ferramenta na xFusionCorp Industries, os administradores de sistema precisam criar uma conta de usuário de serviço. Contas de serviço existem pra rodar processos, não pra login interativo, então normalmente não precisam de diretório home.

## Objetivo
Criar um usuário chamado `rose` no App Server 1 (`stapp01`) sem diretório home.

## O que eu fiz
1. Conectei no servidor alvo: `ssh tony@stapp01`
2. A flag `-M` não estava listada na documentação de User Management do curso, então em vez de arriscar, rodei `useradd --help` pra checar todas as opções disponíveis nesse sistema e localizei `-M, --no-create-home`
3. Primeira tentativa sem privilégios elevados: `useradd -M rose` -> `Permission denied` / `cannot lock /etc/passwd; try again later`
4. Rodei de novo com `sudo`: `sudo useradd -M rose` -> funcionou
5. Validei que o usuário foi criado: `id rose` -> `uid=1001(rose) gid=1001(rose) groups=1001(rose)`
6. Verifiquei o caminho de home registrado no `/etc/passwd`: `grep rose /etc/passwd` -> `rose:x:1001:1001::/home/rose:/bin/bash`
7. Confirmei que o diretório home não existe de fato em disco: `ls /home/` -> só apareceu `tony`, `rose` estava ausente

## Erros e aprendizados no caminho
- Esqueci o `sudo` na primeira tentativa, que falhou com erro de permissão — um lembrete de que `useradd` sempre precisa de privilégios elevados.
- A flag `-M` não está coberta no guia de User Management do curso (que só lista as opções mais comuns). Confirmei que é uma flag legítima checando `useradd --help` direto no sistema, em vez de assumir que não existia só porque não estava na doc.
- Aprendi que o `-M` só impede a pasta física de ser criada — o caminho do home continua sendo registrado no `/etc/passwd` (ex: `/home/rose`) mesmo que o diretório em si nunca exista em disco. Só checar o `/etc/passwd` não é suficiente pra confirmar; é preciso rodar `ls /home/` pra verificar que a pasta realmente não foi criada.
