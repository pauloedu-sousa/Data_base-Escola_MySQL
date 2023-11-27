# Data_base-Escola_MySQL
Foi Realizado a criação do banco de dados MySQL
create database escola;

//Foi Realizado a criação da tabela Aluno

create table aluno(
  id int unsigned not null auto_increment,
  nome varchar(35) not null,
  id_matricula int null,
  email varchar(15) null,
  endereco varchar(20) not null,
  telefone varchar(15) not null,
  PRIMARY KEY (id)
);

//Foi Realizado a criação da tabela Sessão

create table sessao (
  codigo int unsigned not null auto_increment,
  descricao varchar(8) not null,
  localizacao varchar(8) not null,
  PRIMARY KEY (codigo)
);

//Foi Realizado a criação da tabela Livro

create table livro (
  cod_livro int unsigned not null auto_increment,
  titulo varchar(30) not null,
  autor varchar(15) not null,
  cod_sessao int unsigned default null,
  PRIMARY KEY (cod_livro),
  CONSTRAINT fk_livro_sessoes FOREIGN KEY (cod_sessao) REFERENCES
  sessao (codigo)
);

//Foi criado a tabela empréstimo

create table emprestimo (
  codigo int unsigned auto_increment,
  data_hora varchar(15) not null,
  matric_aluno int not null,
  emp_cod_livro int unsigned default null,
  data_devolucao varchar(15)  null,
  PRIMARY KEY (codigo),
  CONSTRAINT fk_emprest_livro FOREIGN KEY (emp_cod_livro) REFERENCES livro (cod_livro)
);


//Foi criado a tabela empréstimo com 2 chaves estrangeiras “ANÁLISE”

create table emprestimo (
  codigo int unsigned auto_increment,
  data_hora varchar(15) not null,
  matric_aluno int unsigned default null,
  emp_cod_livro int unsigned default null,
  data_devolucao varchar(15) not null,
  PRIMARY KEY (codigo),
  CONSTRAINT fk_emprest_aluno FOREIGN KEY (matric_aluno) REFERENCES aluno (id_matricula),
  CONSTRAINT fk_emprest_livro FOREIGN KEY (emp_cod_livro) REFERENCES livro (cod_livro)
);

//Foram inseridos os primeiros dados na tabela aluno

INSERT INTO aluno (nome, id_matricula, email, endereco, telefone)
VALUES ('João Carlos', 1234, 'jcarlos@gmail.com', 'Rua 13 de Maio', '(11)7825-4489');

INSERT INTO aluno (nome, id_matricula, email, endereco, telefone)
VALUES ('José Vitor', 2345, 'jvitor@gmail.com', 'Rua da Saudade', '(11)7825-6589');

INSERT INTO aluno (nome, id_matricula, email, endereco, telefone)
VALUES ('Paulo André', 3456, 'pandr@gmail.com', 'Rua do Sol', '(11)7825-4495');

INSERT INTO aluno (nome, id_matricula, email, endereco, telefone)
VALUES ('Simão Pedro', 2536, 'spedro@gmail.com', 'Rua Santos', '(93)9153-8504');

Foram inseridos os primeiros dados na tabela sessão
insert into sessao (descricao, localizacao) values ('Sessão1', 'Partilheira1');
insert into sessao (descricao, localizacao) values ('Sessão2', 'Partilheira2');
insert into sessao (descricao, localizacao) values ('Sessão3', 'Partilheira3');

//Foram inseridos os primeiros dados na tabela livro

insert into livro (titulo, autor, cod_sessao) values
('O Nome de Jesus', 'Kened Hagin', 1);

insert into livro (titulo, autor, cod_sessao) values
('Como Tomar Posse da Benção', 'RR Soares', 2);

insert into livro (titulo, autor, cod_sessao) values
('O Evangelho Reunido', 'Juan Ribe Pagliarin', 2);

insert into livro (titulo, autor, cod_sessao) values
('Corpo, alma e espírito', 'Kened Hagin', 3);

//Forma realizados os primeiros empréstimos de livros

insert into emprestimo (data_hora, matric_aluno, emp_cod_livro) values ('27/11/2023|08:01:23', 1234, 1);

insert into emprestimo (data_hora, matric_aluno, emp_cod_livro) values ('01/11/2023|10:15:00', 2345, 2);

insert into emprestimo (data_hora, matric_aluno, emp_cod_livro) values ('15/11/2023|14:20:00', 3456, 3);

insert into emprestimo (data_hora, matric_aluno, emp_cod_livro) values ('25/11/2023|09:30:58', 2536, 4);

//Foram Realizadas as primeiras devoluções dos livros emprestados

update emprestimo
set data_devolucao = '27/11/2023|17:18:00'
where codigo = 2;

update emprestimo
set data_devolucao = '26/11/2023|18:18:00'
where codigo = 4;

update emprestimo
set data_devolucao = '25/11/2023|14:35:50'
where codigo = 3;
