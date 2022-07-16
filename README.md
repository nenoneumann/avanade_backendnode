# Carfinder - API

## URL do Projeto:
[Clique aqui](https://carfinder-api.herokuapp.com/)

## Para acessar o swagger:
[Clique aqui](https://carfinder-api.herokuapp.com/swagger/)

## Collections Insomnia:
[Clique aqui](Insomnia_2022-07-04.yaml)

### Projeto exclusivo Avanade <> GamaAcademy

#### Publicando na Azure
-----------------------

Passo 1 criar um fork do projeto para domínio do mesmo, uso. <br>
Passo 2 Provisionar recursos dentro da Azure (App Services) <br>
    - Devemos informar, resource group, nome da aplicação (o nome deve ser único), informar run time, informar sistema operacional e selecionar o tamanou / configuração do hardware alocado.
Passo 3 abrir o repositorio com o projeto para edição do mesmo. <br>
Passo 4 devemos criar as pastas para criar nossa pipeline: diretórios (.github/workflows) arquivo de pipeline (prod.yml) <br>

##### Pipeline template:

```
name: Pipeline CI/CD - Prod

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build-and-deploy: 
    name: Iniciando build e deploy
    runs-on: ubuntu-latest
    environments: production
    steps:
    - uses: actions/checkout@master

    - name: Configurando a versão do NodeJS
      uses: actions/setup-node@v1
      with: 
        node-version: '16.x'

    - name: Estamos instalando dependências e compilando o projeto
      run: |
        npm install
        npm run build --if-preset

    - name: Publicando na Azure
      uses: azure/webapps-deploy@v2
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: .
```


### Professor Douglas Morais
#### Desenvolvido com NodeJS | GamaAcademy