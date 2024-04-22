#  Utilização do Tomcat 10 
FROM tomcat:10

# Copiando o arquivo WAR da aplicação para o diretório padrão de implantação do Tomcat
COPY DimMoneyAppRm99675.war /usr/local/tomcat/webapps/

# Expondo a porta adequada para que a aplicação seja acessível pelo nosso Host
EXPOSE 8080

#Definindo o diretório de trabalho como /usr/local/tomcat/webapps
WORKDIR /usr/local/tomcat/webapps

# Comando padrão a ser executado quando o contêiner é iniciado. 
CMD ["catalina.sh", "run"]
