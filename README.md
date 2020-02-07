# ServicosInfra

## Apache2


1. Primeiro, atualizamos os pacotes do linux

`sudo apt update`

2. Agora, baixamos o apache

`sudo apt install apache2`

3. Abra o navegador e digite "localhost" na barra de pesquisa. Se aparecer uma pagina web com informaçoes sobre o apache, a instalação ocorreu como o esperado.

4. Dentro da pasta /var/www/html crie uma pasta com o nome do seu projeto 

> Ex: /var/www/html/projeto

5. jogue seus arquivos html nesta pagina, alterando o nome da pagina inicial para "index.html", voltando ao navegador, ao digitar localhost novamente, aparecera uma pagina listando as pastas de projeto que voce possui, clickando em uma delas ou acessando localhost/projeto, voce deve conseguir vizualizar sua pagina html.

Caso tenha esquecido de alterar o nome da pagina inicial para index.html, voce pode acessar passando o nome do arquivo, após o nome da pasta

> Ex:localhost/projeto/home.html

-------------------------------------------------------------------------------------------------------------
###Comandos
```
/etc/init.d/apache reload (Recarregar o servidor)
/etc/init.d/apache reload (Para o servidor)
/etc/init.d/apache start (Inicia o servidor)

```
------------------------------------------------------------------------------------------------------------

###Arquivos de Configuração
####Pastas importantes
/etc/apache2 –Pasta com arquivos de configuração
/var/www/html–Pasta Raiz do Site default


/etc/apache2/apache2.conf (Arquivo de configuração principal)
/etc/apache2/ports.conf (Arquivo de configuração da porta do serviço, Porta 80 (http) e 443(https) são as padrões)

 

