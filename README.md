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
### Comandos
```
/etc/init.d/apache reload (Recarregar o servidor)
/etc/init.d/apache reload (Para o servidor)
/etc/init.d/apache start (Inicia o servidor)

```
------------------------------------------------------------------------------------------------------------

### Arquivos de Configuração
#### Pastas importantes
- /etc/apache2 –Pasta com arquivos de configuração
- /var/www/html–Pasta Raiz do Site default


- /etc/apache2/apache2.conf (Arquivo de configuração principal)
- /etc/apache2/ports.conf (Arquivo de configuração da porta do serviço, Porta 80 (http) e 443(https) são as padrões)


-------------------------------------------------------------------------------------------------------------------

## Hosts Virtuais com apache


1. criar diretorios do projeto
`sudo mkdir /var/www/meuprojeto`


criar (ou inserir os arquivos)
`sudo pico /var/www/meuprojeto/index.html` (Seu arquivo html)


2. dar permissoes (alterar usuario e grupo)

```sudo chown -R $USER:$USER /var/www/meuprojeto/
sudo chmod -R 777 /var/www/meuprojeto/
sudo chown -R $USER /var/www/projeto
```



3. config host virtual
- Crie o arquivo com o nome da sua pasta em /var/www;

`sudo touch /etc/apache2/sites-available/meuprojeto.conf` 


- Adicione ao final do arquivo /etc/hosts a seguinte linha:

`127.0.0.2       meuprojeto.com`

com isso, seu navegador irá entender que ao acessar 127.0.0.2, deve redirecionar para a pasta /var/www/meuprojeto

- Volte ao arquivo 
/etc/apache2/sites-available/meuprojeto.conf


e insira no arquivo de configuracao, as seguintes linhas, de acordo com o dominio que voce inseriu em /etc/hosts

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName meuprojeto.com
    ServerAlias meuprojeto.com
    DocumentRoot /var/www/meuprojeto
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Habilite seu host

`
sudo a2ensite meuprojeto.conf
`
- Por fim, reinicie o apache

`systemctl reload apache2`


assim, ao acessar meuprojeto.com em seu navegador, voce sera capaz de vizualizar seus arquivos contidos na pasta /var/www/meuprojeto

 

