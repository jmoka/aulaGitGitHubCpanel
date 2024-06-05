# aulaGitGitHubCpanel
Aula de como se realiza o Deploy para o cpanel, via Git e GitHub

======================================================================


# Deploy Git / cPanel

1. **Criar Conta GitHub**
   - Se você ainda não tem, crie uma conta no GitHub em [github.com](https://github.com).

2. **Criar um Repositório no GitHub**
   - Crie um novo repositório no GitHub. Se for um projeto JavaScript, não é necessário usar o XAMPP. Para projetos WordPress, você precisará do XAMPP.

3. **Instalar o XAMPP**
   - Baixe e instale o XAMPP a partir de [apachefriends.org](https://www.apachefriends.org).

4. **Mudar o Repositório da Pasta htdocs**
   - Copie a pasta `htdocs` para o novo local desejado.
   - Abra o arquivo `httpd.conf` do Apache (localizado em `C:\xampp\apache\conf\httpd.conf`).
   - Localize a diretiva `DocumentRoot` e altere para o novo caminho:
     ```apache
     DocumentRoot "C:/MeusProjetos/htdocs"
     <Directory "C:/MeusProjetos/htdocs">
     ```
   - Reinicie o Apache pelo painel de controle do XAMPP.

5. **Criar um Repositório dentro da Pasta htdocs**
   - No terminal, navegue até a pasta `htdocs` e inicialize um repositório Git:
     ```sh
     cd C:/MeusProjetos/htdocs
     git init
     ```

6. **Criar ou Verificar a Pasta `.ssh` no Caminho**
   - Verifique se a pasta `.ssh` existe em `C:\Users\USUARIO\.ssh`.
   - Se não existir, crie a pasta.

7. **Criar uma Chave SSH**
   - Abra o Prompt de Comando e gere uma nova chave SSH para o Git se conectar com o GitHub:
     ```sh
     ssh-keygen -t ed25519 -C "email do GitHub"
     ```
   - Quando solicitado, deixe a senha em branco e aperte Enter até o final.

8. **Copiar a Chave para o GitHub**
   - Abra a pasta `.ssh` e copie o conteúdo da chave pública (arquivo com extensão `.pub`).
   - No GitHub, vá para `Settings` > `SSH and GPG keys` > `New SSH key`.
   - Dê um título e cole a chave em `Key`, depois salve.

9. **Sincronizar Git com o GitHub**
   - **Configurar Usuário e Email:**
     ```sh
     git config --global user.name "<usuário do GitHub>"
     git config --global user.email "<email do GitHub>"
     ```
   - **Criar Repositório Git na Máquina PC Local:**
    - Escolha a pasta que var ser usada de repositório 
    - Abra oprompt no caminio da pasta e digite:
     ```sh
     git init
     git status
     git add .
     git commit -m "Primeiro Commit de Conexão"
     git branch -M main
     ```
     -Ainda no prompt digite :

   - **Conectar Repositório Remoto:**
     ```sh
     git remote add origin <SSH-do-repositório-GitHub>
     ```
   - **Atualizar o Repositório Remoto com o Local:**
     ```sh
     git pull origin main
     ```
     - **Enviar para o Repositório Remoto do repositorio local:**
     ```sh
     git push origin main
     ```
    - Esses dos comando so são usados a primeira vez , depois :
        - Atualizar
         ```sh
     git pull      
     ```
       - Enviar
         ```sh
     git push      
     ```
        
10. **Configuração no cPanel**
    - **Criar um Repositório:**
      - Abra o gerenciador de arquivos no cPanel.
    - **Criar o SSH:**
      - No cPanel, vá para `Acesso SSH` e abra o terminal.
      - Gere uma chave SSH:
        ```sh
        ssh-keygen -t rsa -f ~/.ssh/crie-um-nome -b 2048 -C "usuariocepanel@url_site_cpanel"
        ```
      - Deixe a senha em branco.
      - Enter

11. **Configuração no Arquivo de Config SSH do cPanel**
    - Abra a pasta `.ssh` e edite o arquivo `config`:
      
    - Adicione ou ajuste as seguintes linhas:
      ```sh
      Host github.com
          User git
          Hostname github.com
          IdentityFile /caminho/da-chave/.ssh/nome_da_chave
          IdentitiesOnly yes
      ```
      
12. **Copiar o Código SSH do cPanel para o GitHub**
    - No cPanel, vá para `Configurações do SSH` e autorize a chave.
    - Copie o código SSH exibido.
    - No GitHub, vá para o repositório, `Settings` > `Deploy keys` > `Add deploy key`.
    - Dê um título, cole a chave e marque `Allow write access`, depois salve.

13. **Configurar Usuário e Email no cPanel**
    - No terminal do cPanel:
      ```sh
      git config --global user.name "usuario_cpanel"
      git config --global user.email "usuario_cpanel@url_site_cpanel"
      ```

14. **Clonar Repositório do GitHub para o cPanel**
    - No cPanel, abra `Git™ Version Control` e crie um novo repositório.
    - Marque `Clone a Repository`, copie o SSH do GitHub e cole no campo `Clone URL`.
    - Coloque o caminho do repositório no cPanel no campo `Repository Path`.
    - Dê um nome para o repositório e crie.

15. **Gerenciar o Repositório no cPanel**
    - Abra `Git™ Version Control`, procure pelo seu repositório, e gerencie.
    - Para atualizar:
      - `Pull or Deploy`
      - `Update From Remote`

16. **Operação diária**
    - Trabalhar no repositório local no PC
    - Realizar os Commites para o GITHUB 
    - Realizar o DEPLOY para o Cpanel