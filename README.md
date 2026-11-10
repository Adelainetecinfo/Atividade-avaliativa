# Atividade-avaliativa
# Sistema Acadêmico — Semana 08 + tratamento global de exceções

Projeto didático Spring Boot (Java 17), PostgreSQL, Flyway, Jakarta Validation e Swagger/OpenAPI.

## Requisitos
- JDK 17 ou superior
- Maven 3.9+
- PostgreSQL

## Banco de dados
Crie o banco antes de iniciar:

```sql
CREATE DATABASE sistema_academico;
```

As credenciais padrão estão em `src/main/resources/application.properties` (usuário `postgres`, senha `postgres`). Se forem diferentes, configure as variáveis `DB_URL`, `DB_USER` e `DB_PASSWORD`. O Flyway cria as tabelas automaticamente na primeira inicialização.

## Executar
Na pasta do projeto:

```bash
mvn spring-boot:run
```

Swagger: http://localhost:8080/swagger-ui.html

## Endpoints principais
- `GET/POST /api/alunos`, `GET/PUT/DELETE /api/alunos/{id}`
- `GET/POST /api/cursos`, `GET/PUT/DELETE /api/cursos/{id}`
- `GET/POST /api/matriculas`, `GET /api/matriculas/{id}`, `PATCH /api/matriculas/{id}/status`
- `GET/POST /api/usuarios`, `GET /api/usuarios/{id}`

## Exemplos para testar
1. Criar aluno: `POST /api/alunos` — `{"nome":"Ana Silva","email":"ana@email.com"}`
2. Criar curso: `POST /api/cursos` — `{"nome":"Análise e Desenvolvimento de Sistemas","descricao":"Curso superior de tecnologia"}`
3. Criar matrícula: `POST /api/matriculas` — `{"alunoId":1,"cursoId":1,"status":"ATIVA"}`
4. Repetir a matrícula ativa do mesmo aluno no mesmo curso: retorna 400 com código `MATRICULA_ATIVA_DUPLICADA`.
5. Consultar `GET /api/alunos/99999`: retorna 404 com código `ALUNO_NAO_ENCONTRADO`.
6. Consultar `GET /api/alunos/abc`: retorna 400.
7. Enviar aluno com nome vazio/e-mail inválido: retorna 400 e lista de campos.
8. Enviar status fora de `ATIVA`, `CANCELADA` ou `CONCLUIDA`: retorna 400 com mensagem controlada.

## Formato de erro
Os erros usam `timestamp`, `status`, `erro`, `mensagem`, `path`, `campos` e `codigo`. O campo `codigo` é o desafio adicional e ajuda o Front-End a identificar o tipo de erro sem depender do texto da mensagem.

## Observações
- O projeto não usa `try/catch` repetitivo nos Controllers: as exceções são encaminhadas ao `GlobalExceptionHandler`.
- A senha de usuário é apenas armazenada neste projeto didático; não há autenticação nem hash implementados. Não use dados reais.
- A estrutura foi criada a partir do enunciado enviado, pois o código original da Semana 08 não foi anexado. Ajuste o pacote ou os campos caso o professor tenha fornecido um modelo anterior específico.


As respostas da tabela de status HTTP, das 10 questões conceituais e a explicação do campo `codigo` estão em `RESPOSTAS_ATIVIDADE.md`.
