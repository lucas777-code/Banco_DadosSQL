# passo a passo: Criação de um banco de dados
Tutorial de como criar um banco de dados sql que organiza as infor,ações de 'livros', 'editora', 'autores e assuntos'.
Este guia sera dividido em etapas para demonstrar desde a criação de tabelas, chaves e ate manipulação/ consulta de dados.

## resumo de uma estrutura SQL
*__CREATE__ para criar 'Banco de dados' ou 'Tabelas'
*__ALTER__ para adicionar ou modificar colunas
*__DROP__ para remover 'Banco de dados' ou 'Tabelas'
*__INSERT__ para atualizar os registros
*__DELETE__ para remover os registros
*__SELECT__ para consultar e visualizar dados

## Passo 1: criação do Banco de Dados e das Tabelas
#### 1.1 Criando o DB

```
CREATE DATABASE biblioteca;
USE biblioteca;
```

### 1.2 Criando a tabela 'editora'
```
CREATE TABLE editora(
    id_editora INT PRIMARY KEY AUTO_INCREMENT,
    nome_editora VARCHAR(100) NOT NULL,
    pais VARCHAR(50)
);
```

#### 1.3 Criando a tabela 'autor'
```
CREATE TABLE autor(
    id_autor INT PRIMAY KEY AUTO_INCREMENT,
    nome_autor VARCHAR(200),
    data_nascimento DATE
);
```

#### 1.4 Criando a tabela 'assunto'
```
CREATE TABLE assunto(
    id_assunto  INT PRIMARY KEY AUTO_INCREMENT,
    descricao_assunto VARCHAR(300)
);
```
#### 1.5 Criando a tabela 'livro'
```
CREATE TABLE livro(
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(150) NOT NULL,
    ano_publicacao YEAR,
    FOREING KEY(id_editora) REFERENCES editora(id_editora),
    FOREING KEY (id_autor) REFERENCES autor (id_autor),
    FOREING KEY (id_assunto) REFERENCES assunto (id_assunto),

);
```
#### 1.6 Criando uma tabela extra
```
CREATE TABLE extra(
    id INT PRIMARY KEY AUTO_INCREMENT,
    produtos VARCHAR (50)
    quantidade INT(20)
    preco DOUBLE NOT NULL

);

```

## Passo 2: editar tabelas usando 'ALTER' 
Após a criação da tabela, podemos adicionar novos campos. Vamos adicionar uma coluna 'email' na tabela 'autor'

```SQL
ALTER TABLE autor
ADD COLUMN email VARCHAR(100);
```

## Passo 3: Remover tabela usando 'DROP'
Se precisar remover uma tabela usamos o comando 'DROP'.
Neste exemplo vamos remover a tabela 'extra'

```SQL
DROP TABLE extra;
```

## Passo 4: Inserindo dados usando 'INSERT'
Agora que as tabelas ja estão prontas, vamos inserir dados nelas.

#### Passo 4.1 Inserindo dados na tabela 'editora'
```SQL
INSERT INTO editora(nome_editora, pais)
VALUES
('Editora Alfa', 'Brasil'),
('Editora Beta', 'Portugal'),
('Editora Bertrand Brasil', 'Brasil');
```

#### 4.2 Inserindo dados na tabela 'autor'
```SQL
INSERT INTO autor(nome_autor, data_nascimento, email)
VALUES
('Jorge Amado', '1912-08-10','jorginho@email.com'),
('Machado de Assis', '1839-06-21','machadinho@email.com'),
('Matt Haig','1975-06-03','matt@email.com');
```

#### 4.3 Inserindo dados na tabela 'assunto'
```SQL
INSERT INTO assunto(descricao_assunto)
VALUES
('Ficção'),
('Misterio'),
('Terror'),
('Romance');
```

## Passo 5: atualizando os dados usando 'UPDATE'
Podemos atualizar os dados com o UPADETE.
Vamos corrigir a data de publicação do livro 'Capitães da Areia'

```SQL
UPDATE livro
SET ano_publicacao = 1938
WHERE titulo = 'Capitães da Areia';
```

## Passo 6: Excluindo os dados usando 'DELETE'
Para remoiver os registros de uma tabela usamos o comando 'DELETE'.
Vamos ecluir o livro 'Memórias Póstumas de Brás Cubas'.

```SQL
DELETE FROM livro
WHERE id_livro = 8;
```

## Passo 7: Consultando os dados usando 'SELECT'
É possivel selecionar os dados para visualizar da forma como quiser.
Para isso usamos o comando 'SELECT'
#### Passo 7.1: selecionar todos os livros com suas editoras e autoras
Vamos uar dados das tabelas 'livros', 'editora', 'autor' e 'assunto'usando o comando 'JOIN'
````SQL
SELECT livro.titulo AS nome,
       editora.nome_editora AS editora,
       autor.nome_autor AS autor,
       assunto.descricao_assunto AS tema,
       livro.ano_publicaco AS ano   
FROM livro
JOIN editora ON livro.id_editora = editora.id_editora.
JOIN autor ON livro.id_autor = autor.id_autor 
JOIN assunto ON livro.id_assunto = assunto.id_assunto;
```

#### Passo 7.2: selecionar todos os livros com o mesmo assunto
Para selecionar todos os livros que pertencem ao mesmo assunto, podemos fazer uma consulta utilizando o comando 'SELECT' com uma condição 'WHERE' especificando o que deseja visualizar.
```SQL
SELECT  livro.titulo AS titulo,
        assunto.descricao_assunto AS tema
FROM livro
JOIN assunto ON livro.assunto = assunto.id_assunto
WHERE assunto.descricao_assunto = 'Romance';