### SQL SERVER

#### Por que armazenar dados? 
É importante armazenar dados e informações para que no futuro eles possam ser reutilizados para que gerem mais dados e mais informações e com isso estar em constante processo de evolução;



#### O que são bancos de dados?

são locais onde os dados e informações são armazenados;



#### O que é um Sistema Gerenciador de Banco de Dados (SGBD) ?

Softwares que padronizam os banco de dados para armazenamento dos dados de maneira organizada;



#### Quais os tipos de bancos de dados?

#### Relacionais (SQL)

- Volume de dados consistente e requer escala média para grande

- Garantias de ACID são necessárias
- Seus dados são previsíveis e altamente estruturados
- Os dados são expressos de maneira relacional
- A segurança de gravação é um requisito
- Você trabalha com consultas e relatórios complexos
- Os usuários são mais centralizados

#### Não-relacionais (NoSQL)

- Alto volume de dados com grande escala
- Suas cargas de trabalho não exigem garantias ACID
- Seus dados são dinâmicos e frequentemente alterados
- Os dados podem ser expressos sem relações
- Você precisa de gravações rápidas e a segurança de gravação não é crítica
- A seleção de dados é simples e tende a ser simples
- Seus dados exigem uma ampla distribuição geográfica



~ obs: **ACID** :  **A**tomicidade, **C**onsistência, **I**solamento e **D**urabilidade;



### ACID

**O que é uma transação?**

> *Uma transação é uma sequência de operações executadas como uma única unidade lógica de trabalho.*

**ACID** é um conceito que se refere às quatro propriedades de transação de um sistema de banco de dados: **A**tomicidade, **C**onsistência, **I**solamento e **D**urabilidade.

- **Atomicidade: ** Em uma transação envolvendo duas ou mais partes de informações discretas, ou a transação será executada totalmente ou não será executada, garantindo assim que as transações sejam atômicas.
- **Consistência:** A transação cria um novo estado válido dos dados ou em caso de falha retorna todos os dados ao seu estado antes que a transação foi iniciada.
- **Isolamento:** Uma transação em andamento mas ainda não validada deve permanecer isolada de qualquer outra operação, ou seja, garantimos que a transação não será interferida por nenhuma outra transação concorrente.
- **Durabilidade:** Dados validados são registados pelo sistema de tal forma que mesmo no caso de uma falha e/ou reinício do sistema, os dados estão disponíveis em seu estado correto.

> Se você desenvolve aplicativos e sistemas corporativos distribuídos as transações ACID serão suas melhores amigas.

As propriedades ACID das transações permitem que você escreva aplicações sem considerar o ambiente complexo em que o aplicativo é executado.

Com transações ACID você pode se concentrar na lógica da aplicação e não na detecção de falhas, recuperação e sincronização do acesso aos dados compartilhados.





#### Comandos

#### Criar Dados (CREATE)

- Criar um banco de dados

```
CREATE DATABASE nome_do_banco;

Exemplo:
CREATE DATABASE escola;
```



- Acessa o banco de dados desejado

```
USE nome_do_banco;

Exemplo:
USE escola
```



- Cria uma tabela com as colunas e seus tipos referenciados;

```
CREATE TABLE nome_da_tabela (				   
	nome_da_coluna tipo_da_coluna				
	nome_da_coluna tipo_da_coluna					
);	 												

exemplo: 	    
CREATE TABLE ESCOLA(
	NOME VARCHAR(50) NULL
	ID INT(5) NOT NULL
);
```



- Tipos de dados SQL

```
Numéricos exatos
bigint					numeric
bit						smallint
decimal					smallmoney
int						tinyint
money

Numéricos aproximados
float 					real

Data e hora
date 					datetimeoffset
datetime2 				smalldatetime
datetime 				time

Cadeias de caracteres
char 					varchar
text

Cadeias de caracteres Unicode
nchar 					nvarchar
ntext

Cadeia de caracteres binária
binary 					varbinary
imagem

Outros tipos de dados
cursor 							rowversion
hierarchyid 					uniqueidentifier
sql_variant 					xml
Tipos de geometria espacial		Tipos de geografia espacial
table
```





#### Alterar dados (ALTER)

- Alterar uma tabela adicionando uma novo coluna

```
ALTER TABLE nome_da_tabela ADD nome_da_coluna tipo_da_coluna;

Exemplo:
ALTER TABLE estudantes ADD idade INT;
```



- Alterar uma tabela modificando uma coluna

```
ALTER TABLE nome_da_tabela MODIFY COLUMN (nome_da_coluna tipo_da_coluna);

Exemplo:
ALTER TABLE estudantes MODIFY COLUMN (id int(6));
```



- Renomear uma coluna em uma tabela

```
sp_rename 'NomeTabela.NomeColunaAntigo', 'NovoNomeColuna', 'COLUMN';

Exemplo:
sp_rename 'estudantes.ID', 'codigo_ID', 'COLUMN';
```



- Renomear uma tabela no banco de dados

```
sp_rename 'NomeTabelaAntigo', 'NomeTabelaNovo';

Exemplo:
sp_rename 'estudantes', 'estudantes_academicos';
```



#### Inserir Dados (INSERT)

- Inserir dados na tabela

```
INSERT INTO nome_da_tabela VALUES (valor1, valor2, ...);

Exemplo: 
INSERT INTO estudantes VALUES ("JOANA", 101515, 16);
```



#### Selecionar Dados (SELECT)

- Seleciona todos os dados de uma tabela

```
SELECT * FROM NOME_DA_TABELA;

Exemplo:
SELECT * FROM estudantes;
```



- Seleciona os dados dos campos específicos de uma tabela

```
SELECT nome_da_coluna, nome_da_coluna FROM nome_da_tabela;

Exemplo: 
SELECT nome, curso FROM estudantes;
```



- Seleciona dados de forma ainda mais refinada

```
SELECT nome_da_coluna FROM nome_da_tabela WHERE nome_da_colunadesejada = "escreva_aqui_o_dado_desejado"

Exemplo: 
SELECT nome FROM estudantes WHERE curso = 'Desenvolvimento de Software';
```



#### Atualizando Dados (UPDATE)

- Setar novo valor a um campo determinado

```
UPDATE nome_tabela SET nome_coluna = 'novo_valor_desejado' WHERE nome_coluna_referencia = "valor_campo";

Exemplo:
SELECT nome FROM estudantes WHERE id = '23'; //Para id=23 exibe o estudante de nome Maria Rosa como exemplo
UPDATE estudantes SET nome = 'Rafael Rodrigues Maia' WHERE id = 23; // Estudante no id=23 passa a ser Rafael
```



#### Deletando Dados (DELETE)

- Deletar dados de uma tabela (não exclui a estrutura da tabela, apenas os registros)

```
DELETE FROM nome_da_tabela;

Exemplo:
DELETE FROM estudantes;
```



- Deletar os dados de uma FILA determinando a posição que se encontra (recomenda-se utilizar como referência colunas como ID ou CPF por exemplo, pois são registros únicos para que não aconteça de se apagar mais de um registro por engano caso aja repetição de valores)

```
DELETE FROM nome_da_tabela WHERE nome_da_coluna_referencia = "valor_do_campo_referencia"

Exemplo:
DELETE FROM estudantes WHERE id = 23;
```



#### Excluir Dados (DROP)

- Excluir uma tabela,, ou seja, toda a estrutura e seus dados

```
DROP TABLE nome_da_tabela;

Exemplo:
DROP TABLE estudantes;
```



- Excluir um banco de dados, ou seja, toda a estrutura bem como suas colunas e seus dados

```
DROP DATABASE nome_do_banco;

Exemplo:
DROP DATABASE escola;
```



## Relação entre tabelas



#### CHAVE PRIMÁRIA

Uma chave que identifica um registro de forma única. Pode ser uma chave única ou composta.



- Declarando chave primaria na criação de uma tabela

```
CREATE TABLE nome_tabela(
	nome_coluna tipo_dado(tamanho) primary_key,
	nome_coluna tipo_dado(tamanho) atributo
);

Exemplo:
CREATE TABLE estudante(
	codigo INT(5) PRIMARY KEY,
	nome VARCHAR(40) NOT NULL
);
```



- Adicionando uma chave primária a uma coluna já criada

```
ALTER TABLE nome_tabela ADD CONSTRAINT nome_chave_Primária PRIMARY KEY (nome_coluna_a_ser_chave_primaria)

Exemplo: 
ALTER TABLE estudantes ADD CONSTRAINT pk_cliente PRIMARY KEY (codigo)
```



#### CHAVE ESTRANGEIRA

Uma chave que identifica a relação entre tabelas. Uma chave estrangeira será sempre uma cópia de uma chave primária a qual faz referência, em outras palavras, uma chave estrangeira é uma chave primária que aponta(referencia) para uma chave primária em outra tabela.



- Adicionando uma chave estrangeira a uma coluna já criada

```
ALTER TABLE nome_tabela ADD CONSTRAINT nome_chave_estrangeira FOREIGN KEY (nome_coluna_a_ser_chave_estrangeira) REFERENCES nome_da_tabela (nome_da_coluna_chave_primaria)

Exemplo: 
ALTER TABLE estudantes ADD CONSTRAINT fk_cliente FOREIGN KEY (codigo) REFERENCES escola (codigoEscola)
```



### Normalização de Dados

##### Primeira Forma Normal (1FN)

- Há apenas atributos monovalorados, singular e não há grupos de atributos repetidos;
- 1FN não aceita atributos multivalorados ou compostos.

Exemplo: 

![tabela desnormalizada, ou seja, não está na primeira forma normal](https://www.luis.blog.br/userfiles/image/1fn_1.gif)

​															*Tabela desnormalizada, ou seja, não está na 1ª forma normal*





![tabela na 1ª forma normal](https://www.luis.blog.br/userfiles/image/1fn_3.gif)

​																							Tabela na 1ª forma normal



![tabela na primeira forma normal](https://www.luis.blog.br/userfiles/image/1fn_4.gif)

​																							*Tabela na 1ª forma normal*



##### Segunda Forma Normal (2FN)

- Atender a 1FN;
- Cada atributo normal e não-chave for total e funcionalmente dependentes da PK;
- 2FN não aceita dependência parcial.

Exemplo:

![tabela não está na segunda forma normal](https://www.luis.blog.br/userfiles/image/2fn_1.gif)

​																				*Tabela não está na segunda forma normal*





![tabela na segunda forma normal](https://www.luis.blog.br/userfiles/image/2fn_2.gif)

​																						*Tabela na segunda forma normal*



![tabela na 2ª forma normal](https://www.luis.blog.br/userfiles/image/2fn_3.gif)

​																						*Tabela na 2ª forma normal*



##### Terceira Forma Normal (3FN)

- Atender a 2FN;
- Um atributo não chave não pode ser determinado por outro atributo não-chave;
- 3FN não aceita dependência transitiva.

Exemplo:

![tabela não está na 3ª forma normal](https://www.luis.blog.br/userfiles/image/2fn_3.gif)

​																				*Tabela não está na terceira forma normal*



![Tabela na terceira forma normal](https://www.luis.blog.br/userfiles/image/3fn_1.gif)

​																					*Tabela na terceira forma normal*







------

Disponibilizado por [thalysson-borges](https://www.linkedin.com/in/thalysson-borges/).

<hr>

fontes: 

https://medium.com/opensanca/o-que-%C3%A9-acid-59b11a81e2c6

https://www.youtube.com/watch?v=--s6RQ3Me3A

https://web.dio.me/course/sql-server-criando-suas-primeiras-consultas/learning/fa84689d-43be-48f2-877c-90ade7932086?back=/track/cognizant-java-developer&tab=undefined&moduleId=undefined

https://blog.betrybe.com/desenvolvimento-web/comandos-sql/#5

http://www.bosontreinamentos.com.br/sql-com-sql-server/como-renomear-colunas-e-tabelas-no-sql-server/

https://docs.microsoft.com/pt-br/sql/t-sql/data-types/data-types-transact-sql?view=sql-server-ver15

