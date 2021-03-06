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
/etc/init.d/apache reload (Reiniciar o servidor)
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

#### Mudando a porta do apache
(aqui estamos alterando a porta do apache de 80 para 3000)
- entre em /etc/apache2/ports.conf e altere a linha "Listen 80" para:
```
Listen 3000

```

- entre em /etc/apache2/sites-enabled/000-default.conf  e altere:
```
<VirtualHost *:3000>
```
e tambem altere 
```
DocumentRoot /var/www/
```

reinicie o serviço



-------------------------------------------------------------------------------------------------------------------

## Hosts Virtuais com apache


1. criar diretorios do projeto
`sudo mkdir /var/www/meuprojeto`


criar (ou inserir os arquivos)
`sudo pico /var/www/meuprojeto/index.html` (Seu arquivo html)


2. dar permissoes (alterar usuario e grupo)

```
sudo chown -R $USER:$USER /var/www/meuprojeto/
sudo chmod -R 777 /var/www/meuprojeto/
```



3. config host virtual
- Crie o arquivo com o nome da sua pasta em /var/www;

`sudo touch /etc/apache2/sites-available/meuprojeto.conf` 


- Volte ao arquivo 
/etc/apache2/sites-available/meuprojeto.conf


e insira no arquivo de configuracao, as seguintes linhas, de acordo com o dominio que voce inseriu em /etc/hosts

```
<VirtualHost *:3000>
    ServerAdmin webmaster@localhost
    ServerName meuprojeto.com
    ServerAlias meuprojeto.com
    DocumentRoot /var/www/meuprojeto
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

obs : Colocamos a porta 3000 aqui pois alteramos a porta padrao do apache para 3000, anteriormente


- Adicione ao final do arquivo /etc/hosts a seguinte linha:

`127.0.0.2       meuprojeto.com`

com isso, seu navegador irá entender que ao acessar 127.0.0.2:3000 ou meuprojeto.com:3000, deve redirecionar para a pasta /var/www/meuprojeto

- Habilite seu host

`
sudo a2ensite meuprojeto.conf
`
- Por fim, reinicie o apache

`systemctl reload apache2`


assim, ao acessar meuprojeto.com em seu navegador, voce sera capaz de vizualizar seus arquivos contidos na pasta /var/www/meuprojeto


## Nginx

- sudo apt-get update
- sudo apt-get install nginx
- sudo /etc/init.d/nginx status
- sudo mkdir /var/www/meuprojetoNginx
- sudo chown -R $USER:$USER /var/www/meuprojetoNginx/
- sudo chmod -R 777 /var/www/meuprojetoNginx/


- sudo nano /var/www/meuprojetoNginx/index.html

- insira seu html

- sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/meuprojetonginx.com

- abra o arquivo criado anteriormente e altere a linha root, deve ficar assim:
```
 server {
        listen   80; ## listen for ipv4; this line is default and implied
        #listen   [::]:80 default ipv6only=on; ## listen for ipv6

        root /var/www/var/www/meuprojetoNginx/;
        index index.html index.htm;

        # Make site accessible from http://localhost/
        server_name example.com;
}
```

` sudo ln -s /etc/nginx/sites-available/meuprojetonginx.com /etc/nginx/sites-enabled/meuprojetonginx.com`

` sudo rm /etc/nginx/sites-enabled/default`

` sudo service nginx restart`

`sudo pico /etc/hosts`

- Insira `172.0.0.1 meuprojetonginx.com` 

## git 

`sudo apt-get update `

`sudo apt-get install git`

`git config --global user.name "Seu Nome"`

`git config --global user.email "exemplo@seuemail.com.br"`

---------------------------------------------------------------------------------------------------------
### Os serviços abaixo form instalados com o Apache configurado para a porta 80, se o seu apache se encontra em outra porta, não se esqueça de informá-la ao acessar o serviço

## PHP 7.4


```
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

`sudo apt install php7.4`

`sudo apt install php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl -y`

`sudo a2enmod php 7.4`

`sudo service apache2 restart`

## Mysql
- Baixar o pacote do site https://dev.mysql.com/downloads/repo/apt/
- instalar o pacote sudo

`dpkg -i mysql-apt-config_0.8.14-1_all.deb`

`sudo apt update`

`sudo apt install mysql-server`

- defina a senha de root
- selecione Use Strong Password Encryption

`sudo systemctl start mysql`

`sudo systemctl enable mysql`

- Instale o workbench, que sera uma ferramenta virtual

`sudo apt install mysql-workbench-community`

- teste a conexao

`sudo mysql -u root -p`


## Phpmyadmin
- O banco de dados deve estar já configurado

`sudo apt-get install phpmyadmin `

- Selecione o Apache como servidor

` mysql -u root -p`

- Insira sua senha escolhida durante a instalaçao do mysql

```
CREATE USER umusuario IDENTIFIED by '<umasenha>';
GRANT ALL PRIVILEGES ON *.* TO 'umusuario'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

`sudo service apache2 restart`

- link o phpmyadmin com a pasta do apache 

`sudo ln -s /usr/share/phpmyadmin /var/www/`

- acesse o phpmyadmin http://localhost/phpmyadmin/ com o usuario criado acima

- Crie um banco utf-8 que será nescessário ao configurar o wordpress

## Moodle

- Faça o download da última versão do moodle em https://download.moodle.org/releases/latest/
- Copie o arquivo para o diretório /var/www
- Acesse o diretório 
- Descompacte o arquivo usando o comando tar xvfz <nomedoarquivo>
- Acesse http://localhost/moodle/, selecione o idioma e prossiga
- Cria uma pasta chamada moodledata onde "Diretório de dados" está indicando
- Dê permissoes a pasta 

`sudo chmod 777 moodledata`

- Reinicie o apache
`/etc/init.d/apache2 restart`

- Recarregue a página do moodle no localhost e prossiga para selecionar MySQL como banco e informar os dados para conexão

- Prossiga para o proximo passo e confira se ha algum erro ou pacote faltando que precise ser instalado ou habilitado



## Wordpress
`wget https://wordpress.org/latest.tar.gz`
 
`tar -zxvf latest.tar.gz`

`sudo mv wordpress/ /var/www/`

`sudo chown www-data.www-data /var/www/wordpress/* -R`
 
`cd /var/www/wordpress/`

`mv wp-config-sample.php wp-config.php`

`sudo pico  wp-config.php`


```
define('DB_NAME', 'seubanco');
define('DB_USER', 'seuuser');
define('DB_PASSWORD', 'suasenha');
define('DB_HOST', 'localhost');
define('DB_CHARSET', 'utf8');
define('DB_COLLATE', '');

```

- acesse http://localhost/wordpress no seu navegador para verificar se o Wordpress está funcionando

- Escolha o idioma e forneça as informaçoes requeridas

- Instale o wordpress
