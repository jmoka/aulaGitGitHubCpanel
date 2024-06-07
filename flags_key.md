# exemplo
## ssh-keygen -t rsa -f ~/.ssh/repo -b 4096 -C "username@example.com"

A flag -b 4096 no comando ssh-keygen especifica o tamanho da chave em bits. Neste caso, 4096 significa que a chave RSA gerada terá 4096 bits de comprimento. Chaves RSA mais longas oferecem mais segurança, mas também podem ser mais lentas para criar e utilizar.

Aqui está um resumo das partes do comando:

ssh-keygen: O comando para gerar chaves SSH.
-t rsa: Especifica o tipo de chave a ser gerada, neste caso, RSA.
-f ~/.ssh/repo: Especifica o arquivo onde a chave será armazenada.
-b 4096: Define o tamanho da chave em bits (4096 bits neste caso).
-C "username@example.com": Adiciona um comentário à chave, geralmente usado para identificar a chave com um endereço de e-mail.
Usar uma chave de 4096 bits é uma prática comum para aumentar a segurança das chaves SSH.


## ssh-keygen -t rsa -f ~/.ssh/crie-um-nome -b 2048 -C "usuariocepanel@url_site_cpanel"

Podendo ser tambémd e 2048 bits

