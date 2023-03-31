# Ambiente de desenvolvimento php5, 7, 8, mariadb, nginx, usado laradock como base
___

## Utilização
3. Instalar docker conforme seu SO
    _ Linux
        _ https://docs.docker.com/engine/install/ubuntu/
    _ Windows
        _ https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe

2. Copiar .env.example para .env
    _ ```
    cp .env.example .env
    ```

3. Editar .env conforme sua estação
    _ Atenção ao env pois todas as variaveis de instalação passam pelo env
    _ Variaveis mais imporantes
        _ APP_CODE_PATH_HOST            => path com os hosts (codigos )
        _ APP_CODE_PATH_CONTAINER       => path em que os hosts vão estar dentro dos containers
        _ DATA_PATH_HOST                => path em que dados estaticos dos containers será salvo no host
        _ PHP_VERSION_8                 => versão do php para container php8
        _ PHP_VERSION_7                 => versão do php para container php7
        _ PHP_VERSION_5                 => versão do php para container php5

4. Na pasta principal execute o comando do compose
    ```
    docker-compose -up --build php5 php7 php8 mariadb nginx
    ```
    _ após os builds são os serviço a serem iniciados
    _ serviços disponiveis php5, php7, php8, mariadb, nginx, portainer