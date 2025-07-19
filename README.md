# Configuração do Projeto Laravel com Docker Compose

Bem-vindo ao guia de configuração manual do seu projeto Laravel com Docker Compose! Este documento irá guiá-lo passo a passo para deixar seu ambiente de desenvolvimento pronto e funcionando.

---

## Pré-requisitos

Certifique-se de ter o Docker e o Docker Compose instalados em sua máquina.

---

## Passos de Configuração

Siga os passos abaixo, executando cada comando no terminal na raiz do seu projeto Laravel (onde o `docker-compose.yml` está localizado).

---

### 1. Construir e Iniciar os Contêineres Docker

Este comando irá construir as imagens Docker (se necessário) e iniciar os serviços definidos no seu `docker-compose.yml` em segundo plano.

```bash
docker compose up -d --build
```

- `up`: Inicia os serviços definidos no `docker-compose.yml`.
- `-d`: Executa os contêineres em modo "detached" (segundo plano), liberando seu terminal.
- `--build`: Força a reconstrução das imagens dos serviços antes de iniciá-los, garantindo que você tenha a versão mais recente do seu código no contêiner.

---

### 2. Instalar Dependências do Composer

Acesse o contêiner da aplicação (laravel-app) e instale as dependências PHP do seu projeto Laravel.

```bash
docker compose exec app composer install
```

- `exec app`: Executa o comando dentro do serviço app (seu contêiner Laravel).
- `composer install`: Instala as dependências PHP definidas no arquivo `composer.json` do seu projeto.

---

### 3. Instalar Dependências do NPM

Acesse o contêiner da aplicação e instale as dependências JavaScript/CSS (Node.js) do seu projeto.

```bash
docker compose exec app npm install
```

- `npm install`: Instala as dependências de frontend definidas no arquivo `package.json`.

---

### 4. Compilar Assets do Frontend

Compile os assets do frontend (JavaScript e CSS) usando o script de build do NPM.

```bash
docker compose exec app npm run build
```

- `npm run build`: Executa o script build configurado no seu `package.json`, geralmente para otimizar e compilar seus assets para produção.

---

### 5. Executar Migrações do Banco de Dados

Execute as migrações do Laravel para criar as tabelas necessárias no seu banco de dados.

```bash
docker compose exec app php artisan migrate
```

- `php artisan migrate`: Executa todas as migrações de banco de dados pendentes do Laravel, criando ou atualizando a estrutura do seu banco de dados.

---

### 6. Gerar a Chave da Aplicação Laravel (APP_KEY)

Gere a chave de segurança da sua aplicação Laravel. Esta chave é crucial para a segurança de sessões, criptografia e outras funcionalidades.

```bash
docker compose exec app php artisan key:generate
```

- `php artisan key:generate`: Gera uma chave aleatória e a define automaticamente no seu arquivo `.env`, garantindo a segurança da sua aplicação.

---

### 7. Iniciar o Servidor de Desenvolvimento Laravel

Finalmente, inicie o servidor de desenvolvimento embutido do Laravel. Este comando manterá o terminal ocupado enquanto o servidor estiver ativo.

```bash
docker compose exec app php artisan serve --host=0.0.0.0 --port=8000
```

- `php artisan serve`: Inicia o servidor de desenvolvimento do Laravel.
- `--host=0.0.0.0`: Permite que o servidor seja acessível de fora do contêiner (via localhost na sua máquina).
- `--port=8000`: Define a porta em que o servidor será executado dentro do contêiner, mapeada para a porta 8000 da sua máquina.

---

## Acessando sua Aplicação

Após o último comando ser executado com sucesso, você poderá acessar sua aplicação Laravel no navegador através de:

http://localhost:8000

---

Para parar o servidor e o contêiner da aplicação, pressione `Ctrl+C` no terminal onde o `php artisan serve` está rodando. Para parar todos os contêineres Docker relacionados ao seu projeto, você pode usar:

```bash
docker compose stop
```
