# aulaGitGitHubCpanel
Aula de como se realiza o Deploy para o cpanel, via Git e GitHub

======================================================================


# Deploy Git / cPanel

## Usando o HTTPS Key 4096

1. **Criar Conta GitHub**
   - Se você ainda não tem, crie uma conta no GitHub em [github.com](https://github.com).
  
2. **Criar uma Key no Cpanel de 4096 bits**
    - Abra o Terminal no Cpanel e digite :
      
      ssh-keygen -t rsa -f ~/.ssh/repo -b 4096 -C "username-cepanel@email_cpanel

3. **Autorize a Key**
    - Após a Chave ser Gerada aperte em Authorize
    - Confirme

4. **Configurar com o GIT**
    - Abra a chave Publica Criada no Cpanel e copie o conteudo
    - Abra o repositório no GITHUB
    - Setings
    - Deploy Keys
    - Add Deploy Key
    - De um Título e Copie a Key do Cpanel já criada e salve.

5. **Criar a conexao com o GITHUB**
    - Crie um Repositório no cpanel e copie o caminho
    - Abra o Git™ Version Control no cpanel
    - Criar
    - Daixar true Clone a Repository
    - Clone URL ( cole o HTTPS do repositório do GITHUB)
    - Repository Path ( Cole o Caminho do repositorio do cpanel)
    - Repository name (De um nome para essa conexão) 

6. **Realizando o Deploy**
    - Abra o Git™ Version Control no cpanel
    - Escolha a conexao e vá em gerenciar
    - Informações Básicas , vá em Atualizar
    - Pull or Deply (Update from remote) - atualização remota
==============================================================

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