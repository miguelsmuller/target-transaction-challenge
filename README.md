# **Transaction Challenge for Target**

O objetivo deste repositório é organizar e gerenciar os projetos relacionados em um único local, facilitando o desenvolvimento, teste e implantação de ambos os projetos.

Este monorepo contém dois projetos relacionados: 

- **[Transaction API](https://github.com/miguelsmuller/transaction-api-for-target)**
- **[Transaction Front](https://github.com/miguelsmuller/transaction-front-for-target)**


## **Estrutura de Submódulos**

Para manter a organização e o versionamento centralizados, este monorepo usa submódulos para incluir os projetos relacionados. Isso permite que você mantenha um histórico de controle de versão compartilhado e mantenha as dependências entre os componentes de maneira consistente.


### **Clonando o Monorepo com Submódulos**

Ao clonar este monorepo, certifique-se de incluir os submódulos para garantir que todos os componentes sejam baixados corretamente:

```shell
git clone --recurse-submodules <monorepo_URL>
```


### **Atualização de Submódulos**

Para atualizar um submódulo específico a partir deste repositório principal, você pode usar os seguintes comandos:

```shell
git submodule update --remote <submodule_name>
ou
git submodule update --remote --recursive
```

Isso trará as últimas mudanças do repositório _<submodule_name>_ e as incorporará no repositório principal.


### **Envio de Alterações nos Submódulos para o Servidor Remoto**

Lembre-se de que ao fazer `git add ...` e `git commit` no monorepo, você está apenas registrando as alterações nos submódulos no histórico do repositório principal. Para enviar as alterações dos submódulos aos seus respectivos repositórios remotos, é necessário executar o comando git push diretamente dentro do diretório do submódulo.


## **Docker Compose**

O arquivo `docker-compose.yml` incluído neste repositório descreve a configuração de um ambiente Docker para executar os projetos. Ele define dois serviços:


### **Serviço Transaction API**

Este serviço é a `Transaction API` que fornece uma API para gerenciar transações.

- Nome do contêiner: transaction-api
- Porta exposta: 5028
- Variáveis de ambiente:
  - ASPNETCORE_ENVIRONMENT=Development


### **Serviço Transaction Front**

Este serviço é o `Transaction Front`, que se conecta à Transaction API e fornece uma interface do usuário para listar e gerenciar transações.

- Nome do contêiner: transaction-front
- Porta exposta: 3090
- Dependências: Dependente do serviço Transaction API
- Variáveis de ambiente:
  - API_URL: URL da API Transaction (http://localhost:5028)


## **Makefile**

Esse projeto possui um Makefile associado para simplificar tarefas comuns de desenvolvimento e inclui as seguinte metas :

- `run`: Inicia o ambiente especificado no docker-compose.yml subindo os container `Transaction API` e `Transaction Front`
