API do Fórum
Este projeto consiste em uma API REST de um Fórum Online construído com Java e alguns módulos do Spring Framework. Todo o código foi escrito como prática e registro do meu aprendizado durante os cursos Spring Boot API REST da Alura, conduzidos pelo instrutor Rodrigo Ferreira .

Como usar
Para testar o projeto, primeiro devemos usar o Maven para instalar as dependências declaradas no pom.xml. Em seguida, devemos indicar quais configurações de ambiente queremos subir a aplicação: dev , test ou prd . Se estivermos rodando o projeto diretamente de um IDE, podemos indicar isso da seguinte forma:

// No Eclipse: Run Canfigurations -> “VM arguments”
-Dspring.profiles.active.dev

// No IntelliJ: Run -> Edit Configurations -> "Program arguments"
--spring.profiles.active=dev
Além disso, se as configurações de prd foram indicadas, devemos fornecer as variáveis ​​de ambiente para o banco de dados e para o segredo da geração de tokens JWT (essas variáveis ​​envolvidas logo abaixo). Assim, uma outra opção é fazer o build do projeto e rodar a aplicação a partir de um arquivo .jar, bastando executar mvn clean packagee em seguida:

java \  
  -DFORUM_DATABASE_URL=DATABASE:h2:mem:forumdb \ 
  -DFORUM_DB_USERNAME=sa \
  -DFORUM_DB_PASSWORD= \
  -DFORUM_JWT_SECRET=123456 \
  -Dspring.profiles.active.prd \
  -jar forum-api-0.0.1-SNAPSHOT.jar \
  /
Por fim, o projeto também conta com um Dockerfileque permite construir uma imagem e subir uma aplicação em um container com Docker :

docker build . -t forum/forum-api

docker run \
  -p 8080:8080 \
  -e FORUM_DATABASE_URL='DATABASE:h2:mem:forumdb' \
  -e FORUM_DB_USERNAME='sa' \
  -e FORUM_DB_PASSWORD='' \
  -e FORUM_JWT_SECRET='123456' \
  -e SPRING_PROFILES_ACTIVE='prd' forum \
  /forumapi \
  /
Para conhecer todos os endpoints e como montar as requisições, basta acessar localhost:8080/swagger-ui.html. Em dev , todos os endpoints estão abertos e não desabilitam autenticação. Em prd , no entanto, é preciso gerar um token JWT POST /authpara que seja possível fazer outras requisições.

Tópicos
Alguns dos tópicos estudados durante o curso e implementados neste código:

Exposição de endpoints com@RestController
Uso dos padrões DTOe Formpara entrada e saída de dados
Spring Datae Hibernatepara persistência, busca e manipulação de dados
Montagem de respostas comResponseEntity
Validação de dados comBean Validation
Tratamento de exceções com@RestControllerAdvice
Paginação e ordenação com Pageable, DirectioneSpringDataWebSupport
Cache com @Cacheablee@CacheEvict
Configurações de autenticação e autorização comSpring Security
Geração e validação de JWT com lib jjwte filtroOncePerRequestFilter
Monitoramento com Spring Boot ActuatoreSpring Boot Admin
Documentação comSpringFox Swagger
Configurações de ambientes com@Profile
Testes automatizados dos beans do Spring com @SpringBootTest, @DataJpaTesteMockMvc
Construa e implante a aplicação com MaveneDocker
