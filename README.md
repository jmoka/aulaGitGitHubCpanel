# aulaGitGitHubCpanel
Aula de como se realiza o Deploy para o cpanel, via Git e GitHub

======================================================================


# Deploy Git / cPanel

1. **Criar Conta GitHub**
   - Se você ainda não tem, crie uma conta no GitHub em [github.com](https://github.com).

2. **Criar um Repositório no GitHub**
   - Crie um novo repositório no GitHub. Se for um projeto JavaScript, não é necessário usar o XAMPP. Para projetos WordPress, você precisará do XAMPP.

3. **Criar ou Verificar a Pasta `.ssh` no Caminho**
   - Verifique se a pasta `.ssh` existe em `C:\Users\USUARIO\.ssh`.
   - Se não existir, crie a pasta.

4. **Criar uma Chave SSH**
   - Abra o Prompt de Comando e gere uma nova chave SSH para o Git se conectar com o GitHub:
    
     ssh-keygen -t ed25519 -C "email do GitHub"
   
   - Quando solicitado, deixe a senha em branco e aperte Enter até o final.

5. **Copiar a Chave para o GitHub**
   - Abra a pasta `.ssh` e copie o conteúdo da chave pública (arquivo com extensão `.pub`).
   - No GitHub, vá para `Settings` > `SSH and GPG keys` > `New SSH key`.
   - Dê um título e cole a chave em `Key`, depois salve.

6. **Sincronizar Git com o GitHub**
   - **Configurar Usuário e Email:**
    
     git config --global user.name "<usuário do GitHub>"
     git config --global user.email "<email do GitHub>"
     
   - **Criar Repositório Git na Máquina PC Local:**
    - Escolha a pasta que var ser usada de repositório 
    - Abra oprompt no caminio da pasta e digite:
   
     git init
     git status
     git add .
     git commit -m "Primeiro Commit de Conexão"
     git branch -M main

     -Ainda no prompt digite :

   - **Conectar Repositório Remoto:**
    
     git remote add origin <SSH-do-repositório-GitHub>
    
   - **Atualizar o Repositório Remoto com o Local:**
     
     git pull origin main
   
     - **Enviar para o Repositório Remoto do repositorio local:**
    
     git push origin main
     
    - Esses dos comando so são usados a primeira vez , depois :
        - Atualizar
         
     git pull      
     
       - Enviar
        
     git push      
     
        
7. **Configuração no cPanel**
    - **Criar um Repositório:**
      - Abra o gerenciador de arquivos no cPanel.
    - **Criar o SSH:**
      - No cPanel, vá para `Acesso SSH` e abra o terminal.
      - Gere uma chave SSH:
        
        ssh-keygen -t rsa -f ~/.ssh/crie-um-nome -b 2048 -C "usuariocepanel@url_site_cpanel"
      
      - Deixe a senha em branco.
      - Enter

8. **Configuração no Arquivo de Config SSH do cPanel**
    - Abra a pasta `.ssh` e edite o arquivo `config`:
      
    - Adicione ou ajuste as seguintes linhas:
 
      Host github.com
          User git
          Hostname github.com
          IdentityFile /caminho/da-chave/.ssh/nome_da_chave
          IdentitiesOnly yes
    
      
9. **Copiar o Código SSH do cPanel para o GitHub**
    - No cPanel, vá para `Configurações do SSH` e autorize a chave.
    - Copie o código SSH exibido.
    - No GitHub, vá para o repositório, `Settings` > `Deploy keys` > `Add deploy key`.
    - Dê um título, cole a chave e marque `Allow write access`, depois salve.

10. **Configurar Usuário e Email no cPanel**
    - No terminal do cPanel:
     
      git config --global user.name "usuario_cpanel"
      git config --global user.email "usuario_cpanel@url_site_cpanel"
     

11. **Clonar Repositório do GitHub para o cPanel**
    - No cPanel, abra `Git™ Version Control` e crie um novo repositório.
    - Marque `Clone a Repository`, copie o SSH do GitHub e cole no campo `Clone URL`.
    - Coloque o caminho do repositório no cPanel no campo `Repository Path`.
    - Dê um nome para o repositório e crie.

12. **Gerenciar o Repositório no cPanel**
    - Abra `Git™ Version Control`, procure pelo seu repositório, e gerencie.
    - Para atualizar:
      - `Pull or Deploy`
      - `Update From Remote`

13. **Operação diária**
    - Trabalhar no repositório local no PC
    - Realizar os Commites para o GITHUB 
    - Realizar o DEPLOY para o Cpanel


    ========================================================
    # RESOLVENDO CONFLITOS
    - EM ALGUM MOMENTO VC VAI FAZER UM DEPLOY E SEU REPOSITÓRIO NO CPANEL ESTÁ DIFERENTE DO QUE ESTA SENDO ENVIADO, OU SEJA HOUVE UM MUDANCA NO CPANEL SEM ESTÁ TRAKEADO
    - PARA RESOLVER ESSA SITUAÇÃO É O SEGUINTE

    "Esse erro ocorre porque você está tentando fazer um merge (ou outra operação similar) em um repositório Git que tem alterações locais não comprometidas em arquivos específicos (.htaccess e wp-config.php). O Git não permite que você faça o merge enquanto essas alterações não forem resolvidas para evitar perder essas mudanças."

    # Cometer as mudanças locais:
      - Se você deseja manter as alterações locais, você pode cometer essas mudanças antes de tentar o merge novamente.

      ## CODIGO
                git add .htaccess wp-config.php
                git commit -m "Sua mensagem de commit descrevendo as mudanças"
                git merge [nome_da_branch_ou_commit]
        ### EXEMPLO
                git add .htaccess wp-config.php
                git commit -m "Updated .htaccess and wp-config.php"
                git merge origin/main

    # Fazer stash das mudanças locais:
      - Se você não deseja cometer as alterações agora, você pode fazer stash delas. Isso salvará temporariamente as suas mudanças para que você possa aplicá-las mais tarde.

      ## CODIGO
                git stash push -m "Salvando mudanças temporariamente"
                git merge [nome_da_branch_ou_commit]
                git stash pop
        ### EXEMPLO
                git stash push -m "Stashing changes before merge"
                git merge origin/main
                git stash pop
        
    # Descartar as mudanças locais:
      - Se você não precisa dessas mudanças locais, você pode descartar as alterações.

      ## CODIGO
                git checkout -- .htaccess wp-config.php
                git merge [nome_da_branch_ou_commit]
        ### EXEMPLO
                git checkout -- .htaccess wp-config.php
                git merge origin/main