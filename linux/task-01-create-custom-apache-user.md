# Task 1 — Create Custom Apache User (Linux User Management)

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
