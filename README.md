# Ambiente de desenvolvimento php5, 7, 8, mariadb, nginx, usado laradock como base
___
## Estrutura
![alt text](https://github.com/Lydia-Sistemas/dev-docker/blob/main/img/ex1.png?raw=true)
## Utilização
1. **Instalar docker conforme seu SO**
    - Linux
        -  https://docs.docker.com/engine/install/ubuntu/
    - Windows
        - https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe

2. **Copiar .env.example para .env**
    ```
    cp .env.example .env
    ```

3. **Editar .env conforme sua estação**
    - Atenção ao env pois todas as variaveis de instalação passam pelo env
    - Variaveis mais imporantes
        - **APP_CODE_PATH_HOST**            => path com os hosts (codigos )
        - **APP_CODE_PATH_CONTAINER**       => path em que os hosts vão estar dentro dos containers
        - **DATA_PATH_HOST**                => path em que dados estaticos dos containers será salvo no host
        - **PHP_VERSION_8**                 => versão do php para container php8
        - **PHP_VERSION_7**                 => versão do php para container php7
        - **PHP_VERSION_5**                 => versão do php para container php5
4. **Cria as seguintes diretórios no caminho que você indicou em DATA_PATH_HOST**
    - /nginx/sites/
    - /logs/nginx/
    - /mariadb/
    - /portainer_data/
4. **Na pasta principal execute o comando do compose**
    ```
    docker-compose -up --build php5 php7 php8 mariadb nginx
    ```
    - Após os builds são os serviço a serem iniciados
    - Serviços disponiveis php5, php7, php8, mariadb, nginx, portainer
5. **Caso escolhe por iniciar o portainer acesse pelo endereço abaixo**
    - http://localhost:9010
6. **Para configurar NGINX**
    - Adicione um arquivo conf do nginx no path DATA_PATH_HOST/nginx, DATA_PATH_HOST caminho que você indicou no .env
        - Exemplo de configuraçao dos hosts
        ```
        server {
            server_name php.local;
            root /sources/;

            location = / {
                try_files @site @site;
            }

            location / {
                try_files $uri $uri/ @site;
            }

            location ~ \.php$ {
                return 404;
            }

            location @site {
                fastcgi_pass php8:9000;
                include fastcgi_params;
                fastcgi_param  SCRIPT_FILENAME $document_root/index.php;
                #uncomment when running via https
                #fastcgi_param HTTPS on;
            }

            error_log /var/log/nginx/error.log;
            access_log /var/log/nginx/access.log;
        }
        ```
    - Após adicionar um novo host (site) reinicie o container do **nginx**
    - ***fastcgi_pass*** indica o nome do container a ser utilizado com qual versão do php, no exemplo utilizando ***php 8***
