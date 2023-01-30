# MySQL - Bancode Dados

Para criar banco de dados:

    CREATE DATABASE cadastro;

* tanto faz escrever maiúsculo ou minúsculo

Um banco de dados contém tabelas, tabelas contém registros e registros são compostos por campos.

===================================================

    Create table pessoas (
        nome,
        idade,
        sexo,
        peso,
        altura,
        nacionalidade
    );

===================================================

Tipos primitivos:

- Numérico;
- Data/Tempo;
- Literal;
- Espcial

            Inteiro: TinyInt, smallInt, Int, MediumInt, BigInt
Numéricos:  Real: Decimal, float, Double, Real
            Lógico: Bit, Boolean

Data / Tempo: Date, DateTime, TimeStamp, Time, Year


            Caractere: Char, VarChar
            Texto: tinyText, Text, MediumText, LongText
Literal:
            Binário: TinyBlob, Blob, MediumBlob, LongBlob
            Coleção: Enum, Set

Espacial: Geometry, Point, Polygon, MultiPolygon

===================================================

    Create table pessoas (
        nome varchar(30),
        idade tinyInt(3),
        sexo char(1),
        peso float,
        altura float,
        nacionalidade varchar(20)
    );

===================================================

* Use nome_do_banco = ativa o banco
* describe pessoas;
* drop database nome_do_banco = apaga o banco

- Os parametros no mysql se chama constraints

===================================================

    create database cadastro
    default character set utf8
    default collate utf8_general_ci;

===================================================

### Melhorando a criação de banco de dados.

    Create table pessoas (

        nome varchar(30) Not null,
        nascimento date *colocar a data de nascimento, pois a idade muda todo ano*
        sexo enum ('M', 'F'),
        peso decimal (5,2) *5 casas sendo 3antes da virgula e 2 depois*
        altura decimal (3,2) *1 casa antes da virgula e 2 depois*
        nacionalidade varchar(20) default 'Brasil' *Deixa como padrão o Brasil*

    )defult charset = utf8;

Contraints do código acima (not null e default)

    Create table pessoas (

        id int not null auto_Increment,
        nome varchar(30) Not null,
        nascimento date *colocar a data de nascimento, pois a idade muda todo ano*
        sexo enum ('M', 'F'),
        peso decimal (5,2), *5 casas sendo 3antes da virgula e 2 depois*
        altura decimal (3,2), *1 casa antes da virgula e 2 depois*
        nacionalidade varchar(20), default 'Brasil' *Deixa como padrão o Brasil*
        Primary Key (id) *Faz existir um id único por pessoa*

    )defult charset = utf8;

- auto_increment - significa que automaticamente o sistema vai definir que o id da primeira pessoa cadastrada seja 1, o segundo2, o terceiro 3 e assim sucessivamente.

- Comando DDL(Data Definition Language) - Create table, Create database

=====================================

    insert into pessoas 
    (nome, nascimento, sexo, peso, altura, nacionalidade)
    values
    ('Godofredo', '1984-01-02', 'M', '78.5', '1.83', 'Brasil');

Esse é o caomnado para inserir dados na tabela.

Lembrando que não é necessário colocar o id, pois utilizamos a constraint auto_increment, e com isso o sistema define o id.

Se quisermos colocar o campo Id podemos colocar a constraint default, por conta do auto_increment:

insert into pessoas
(id, nome, nascimento, sexo, peso, altura, nacionalidade)
values
(default, 'Creuza', '1920-12-30', 'f', '50.2', '1.65', 'default');

Nesse caso com default no id ele puxa o auto_increment.
E no caso da nacionalidade ele puxa o Brasil, pois definimos ele como padrão para nacionalidade.

=====================================

Select * from pessoas; => comando para ver o conteúdo do tabela pessoas.

Caso os dados forem adicionados de acordo com a ordem que está no banco de dados, não é necessário colcoar os nomes doas campos, exemplo:

    insert into pessoas(nome_da_tabela) values
        (default, 'adalgiza', '1930-11-02', 'f', '63.2', '1.75', 'Irlanda');

Podemos colocar vários dados também de uma vez:

    insert into pessoas(nome_da_tabela) values
        (default, 'adalgiza', '1930-11-02', 'f', '63.2', '1.75', 'Irlanda'),
        (default, 'Allisson', '2000-11-16', 'M', '75.3', '1.78', 'Brasil'),
        (default, 'Ronaldo', '1980-11-02', 'M', '85.9', '1.85', 'Portugal');

Com isso ele irá mandar todos os dados de uma vez.

insert into } DML - Data Manipulation Language
Não serviu para definir algo (DDl) e sim para manipular os dados no banco (DML).

=====================================

Alter table pessoas => serve para alterar a tabela

Add column profissao varchar(10); => adiciona coluna com nome profissao

describe pessoas pode ser escrita de forma mais curta => desc pessoas;

alter table pessoas drop column profissao; => deleta coluna profissao.

====================================

Alter table pessoas add column profissao varchar(10) after nome; => adiciona uma coluna com o nome profissão depois da coluna chamada nome.

*Não existe comnado before, apenas after.*

Caso quiser adiconar alguma coluna no começo da tabela utilizamos:

    Alter table pessoas add column codigo int first;

===================================

Alter table pessoas modify column profissao varchar (20);

O comando acima modifica o tipo e pode redefinir as constraints, mas não pode alterar o nome da coluna.

==================================

Para trocar o nome da coluna utilizamos:

    Alter table pessoas change column profissao prof varchar (20);

==================================

Para alterar o nome da tabela inteira:

    Alter table pessoas rename to gafanhotos

==================================

    Create table if not exists cursos (

        nome varchar(30) not null unique, => unique significa campo obrigatório e com nome único
        descrica text,
        carga int unsigned,
        totaulas int,
        ano year default '2016'

    )default charset = utf8;

*Unsigned* => sem sinal, ele vai economizar 1 bite para cada registro que tenha a carga registrada

*if not exist* => serve para não criarmos uma tabela com mesmo nome, caso isso aconteça ele vai apagar a primeira e sobrescrever essa nova.

=================================

alter table cursos add primary key(id cursos);

drop table cursos; => apaga a tabela cursos.

Alter table => DDL
Drop table => DDL

==================================

    Update cursos set nome = 'HTML5' where idcursos = '1'; 

O código acima altera o texto de nome na linha de idcurso 1.

    Upadte cursos set nome = 'PHP', ano = '2015' where idcursos = 4';

O código acima altera os valores em duas colunas diferentes na mesma linha

    Update cursos set nome = 'JAVA', carga = '4', ano = '2015' where idcursos = '5' limit 1;

O código acima altera 3 colunas.

*Limit 1;* => Limita quantas linhas podem ser afetadas, isso é uma segurança para não afetar mais de uma linha caso eu erre o comando.

==============================

delete from cursos where idcursos = '8';

=============================

truncate table cursos; => apaga todas as linhas do curso.

==============================

upadate, delete, truncate => DML

==============================

Show tables; => mostra as tabelas existentes dentro do banco de dados.

*TERMINAL*

comando Status => serve para saber qual banco de dados está aberto no momento.

    show create table amigos;

O código acima serve para você ver os comandos utilizados para criar a tabela amigos nesse caso.










