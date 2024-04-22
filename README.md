# Implantação de Aplicação Java Web no Tomcat usando Docker

Este repositório contém os passos necessários para implantar uma aplicação Java Web simples no servidor Tomcat 10 usando Docker.

## Pré-requisitos

- Docker instalado e configurado em sua máquina.

## Passos

### 1. Clonar o repositório:

```bash
git clone https://github.com/Fabs0602/desafio-devops-java.git
````
### 2. Modificar o código fonte:
- Modifique o arquivo index.jsp para alterar a mensagem que será exibida na tela.
- Exporte o arquivo .War e salve no diretório root do projeto
  
### 3. Criar o Dockerfile:
- Crie um Dockerfile com as seguintes instruções:
````dockerfile
# Use o Tomcat 10 como imagem base
FROM tomcat:10

# Copie o arquivo WAR da aplicação para o diretório padrão de implantação do Tomcat
COPY <nomeArquivoWar>.war /usr/local/tomcat/webapps/

# Exponha a porta adequada para que a aplicação seja acessível pelo nosso Host
EXPOSE 8080

# Defina o diretório de trabalho como /usr/local/tomcat/webapps
WORKDIR /usr/local/tomcat/webapps

# Rode o Tomcat
CMD ["catalina.sh", "run"]
````

### 4. Criar volume:
- Caso não possua um volume criado, criar um volume chamado deploys-tomcat10
````docker
docker volume create deploys-tomcat10
````

### 5. Construir a imagem Docker:
- Construa a imagem Docker executando o seguinte comando dentro do diretório do projeto:
````docker
docker build -t <nomeDaImagem> .
````

### 6. Rodar o conteiner:
- Roda o contêiner a partir da imagem criada:
````docker
docker run -d -p 8080:8080 --name <nomeDoContainer> <nomeDaImagem>
````

### 7. Ver logs da aplicação do TomCat:
````docker
docker logs <nomeDoContainer>
````

### 6. Acessar a aplicação:
- Acesse a aplicação no navegador:
````bash
http://localhost:8080/<nomeArquivoWar>/
````

###  8. undeploy dessa aplicação pelo Volume do Host:
Para undeploy da aplicação, remova o arquivo .War:
````docker
# Removendo o arquivo WAR do volume
docker exec <nomeDaImagem> rm /usr/local/tomcat/webapps/<nomeDoArquivoWarAntigoASerRemovido>.war
````

### 7. Redeploy e Modificação da aplicação :
- Modifique o código fonte conforme necessário sempre exportando um novo arquivo .War
- Atualize o DockerFile com o nome do arquivo .War (Caso o nome seja diferente do anterior)
- Faça o undeploy antes do redeploy
- Para o redeploy iremos basicamente copiar o arquivo .war novo para o volume que já temoscriado
  
````docker
# Copiando o novo arquivo WAR para o contêiner em execução
docker cp <nomeArquivoWar>.war <nomeDoVolume>:/usr/local/tomcat/webapps/
````

### Integrantes do grupo
<table>
  <tr>
        <td align="center">
      <a href="https://github.com/biancaroman">
        <img src="https://avatars.githubusercontent.com/u/128830935?v=4" width="100px;" border-radius='50%' alt="Bianca Román's photo on GitHub"/><br>
        <sub>
          <b>Bianca Román</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/charlenefialho">
        <img src="https://avatars.githubusercontent.com/u/94643076?v=4" width="100px;" border-radius='50%' alt="Charlene Aparecida's photo on GitHub"/><br>
        <sub>
          <b>Charlene Aparecida</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/laiscrz">
        <img src="https://avatars.githubusercontent.com/u/133046134?v=4" width="100px;" alt="Lais Alves's photo on GitHub"/><br>
        <sub>
          <b>Lais Alves</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/LuccaRaphael">
        <img src="https://avatars.githubusercontent.com/u/127765063?v=4" width="100px;" border-radius='50%' alt="Lucca Raphael's photo on GitHub"/><br>
        <sub>
          <b>Lucca Raphael</b>
        </sub>
      </a>
    </td>
     <td align="center">
      <a href="https://github.com/Fabs0602">
        <img src="https://avatars.githubusercontent.com/u/111320639?v=4" width="100px;" border-radius='50%' alt="Fabricio Torres's photo on GitHub"/><br>
        <sub>
          <b>Fabricio Torres</b>
        </sub>
      </a>
    </td>
  </tr>
</table>

