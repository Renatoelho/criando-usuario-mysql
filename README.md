# Criando usuário no MySQL

Vou ensinar como criar um usuário no *MySQL*, pois não é recomendado utilizar o usuário ````root```` para o desenvolvimento. Esse passo a passo vai possibilitar também a segmentação de acessos e o que pode ou não ser acessado pelo usuário em questão.

#### Versão do MySQL que foi utilizada nesse passo a passo: 
> *Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)*

Todos os comandos listados aqui devem ser executados pelo usuário ````root```` ou outro com poderes equivalentes.

# Criando usuário

### Sintaxe: 

````
create user '<usuário>'@'<acesso a partir de...>' identified by '<senha>’; 
````

Vamos dar o nome para o usuário de ````user01```` e permitir seu acesso a partir de qualquer origem, para isso adicione ````'%'```` depois do sinal de ````@````.

````
create user 'user01'@'%' identified by '12345';
````

![Criação usuário user01](https://drive.google.com/uc?export=view&id=1MZ5LD4yfsgxkXHvHnHlh3my83tRcxpv3)

# Permissões para o usuário

Para dar as permissões necessárias execute a seguinte *query*, considerando que o usuário ````user01```` terá todas as permissões, caso queira limitar isso altere o parâmetro ````all```` por outro como ````select````, ````create```` e etc, além de acesso somente às tabelas do database ````sistema01````.

### Sintaxe: 

````
grant <permissões> privileges on <database>.<tabelas> to '<usuário>'@’<a partir de>’;
````

````
grant all privileges on sistema01.* to 'user01'@'%';
````

![Permissões para o Usuário](https://drive.google.com/uc?export=view&id=1Ma3YpSIa0bVv9VTm73izyExp4-XYJcgS)

> **Observação:** caso queira que a regra de um determinado parâmetro seja aplicada de maneira abrangente passe um asterisco ````*```` como parâmetro, se preferir que o usuário ````user01```` tenha acesso a todos os databases é só passar o ````*```` no lugar do ````sistema01````. 

# Atualizando o sistema de permissões

Para atualizar a tabela que gerencia os privilégios do sistema execute a seguinte ***query***:

````
flush privileges;
````

![Atualizando Privilégios](https://drive.google.com/uc?export=view&id=1Md0pjJMA0aWkgdjfGac89WZcuMt9_Cxb)

# Testando o acesso do novo usuário.

````
mysql -u user01 -p
````

![Acesso novo usuário](https://drive.google.com/uc?export=view&id=1Mgd9T4aRRxZ6vH9yWO8i7OnCztYQK9bI)

Pronto! Usuário criado e permissões atribuídas, caso queira mais detalhes das opções existentes na sintaxe do *MySQL* acesse a documentação listada nas referências. 

**Referências:**  <br/><font size="1">  <br/>Dev.mysql.com, **Account Management Statements.** Disponível em: <https://dev.mysql.com/doc/refman/8.0/en/account-management-statements.html>. Acesso em: 18 nov. 2021.  <br/>Dev.mysql.com, **CREATE USER Statement.** Disponível em: <https://dev.mysql.com/doc/refman/8.0/en/create-user.html>. Acesso em: 18 nov. 2021.  <br/>Dev.mysql.com, **GRANT Statement.** Disponível em: <https://dev.mysql.com/doc/refman/8.0/en/grant.html>. Acesso em: 18 nov. 2021.  <br/></font>
