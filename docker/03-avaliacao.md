# Docker compose com Django e banco de dados

## Informações gerais

- Assunto: Docker, conteinizar aplicativos
- Disciplina: *sistemas operacionais*
- **Tarefa**:
  1. Criar um projeto django com uma aplicação web
    - alternativa, criar uma _branch_ no repositório do projeto integrador para configurar o acesso ao repositório de dados
  2. Criar um `Dockerfile` para o projeto django
  3. Criar a imagem e testar o conteiner para testar
  4. OPCIONAL, porque dependendo de como pergunta ao assistente de IA; criar um `Dockerfile` para o repositório de banco de dados
  5. Criar um `docker-compose.yml` e configurar para 2 serviços: `webapp` e `db`
  6. Configurar o arquivo django de acesso ao repositório de dados para usar o serviço docker `db`
  7. Testar o `docker-compose.yml`
  8. Relatar minimamente o que foi feito.
- **Entrega**: copia desse aquivo markdown preenchido, no seu repositório _fork_ de https://github.com/sistemas-operacionais/2024.2


## Relatório

### Aluno

- nome: Agnes G Barbosa
- matrícula: 20232014040023

### Relato
Fiz a integração no meu projeto do PDS: Arkheion.
Primeiro de tudo trouxe o arquivo ```requirements.txt``` para o diretório do mysite, o projeto.
Depois, criei o arquivo ```Dockerfile``` e o ```docker-compose.yml```. Testamos se rodou, não rodou. Estava dando erro ao copiar o ```requirements.txt```. Como eu não sabia exatamente o que era necessário manter para rodar a aplicação e o arquivo tinha cerca de 600~700 linhas, perguntei ao Deepseek quais eu deveria manter e ele limpou, deixando apenas os principais.
Logo em seguida, dei o comando ```docker-composer up --build``` pra iniciar e buildar o docker, usando o comando descrito no arquivo ```docker-composer.yml```: bash -c "python manage.py migrate && python manage.py runserver 0.0.0.0:8000" para abrir o servidor e realizar as migrações dos models para o banco.

### Arquivos docker e de configuração do django

## Dockerfile
FROM python:3.12
WORKDIR /mysite
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

## docker-compose.yml
services:
    app:
        build: .
        container_name: arkheion
        command: bash -c "python manage.py migrate && python manage.py runserver 0.0.0.0:8000"
        ports: 
            - "8000:8000"

**observação** coloque nomes nos arquivos antes do códigos-fonte.
