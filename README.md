# SQL-Database-afterschool

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Tools used: MySQL Workbench

Application under test: afterschool SQL

Database description: It is a database for an afterschool containg data about students, parents, teachers, grades and the relatuonships between them.

1.Database Schema

You can find below the database diagram that was generated through Reverse Engineer and which contains all the tables and the relationships between them.

![SQL Diagram](https://github.com/armandaskalu/SQL-Database-afterschool/blob/main/SQL%20Diagram.jpg)

2.Database Queries

2.1. DDL (Data Definition Language)

The following instructions were written in the scope of creating the structure of the database:

create database afterschool;
use afterschool;

create table elevi
(idelev int not null auto_increment primary key,
numeelev varchar(50) not null,
clasa int not null);

create table parinti
(idparinte int not null auto_increment primary key,
numeparinte varchar(50) not null,
idelev int not null,
clasa int not null);
create table profesori
(idprof int not null auto_increment primary key,
numeprof varchar(50) not null,
materie varchar(50) not null);

create table note
(idnota int not null auto_increment primary key,
ziua date,
idelev int not null,
idprof int not null,
materie varchar(50) not null,
nota int not null);

create table absente
(idnota int not null auto_increment primary key,
ziua date,
idelev int not null,
idprof int not null,
materie varchar(50) not null,
prezent bool);

After the database and the tables have been created, a few ALTER instructions were written in order to update the structure of the database, as described below:

alter table parinti
drop column clasa;

alter table parinti
add foreign key (idelev) references elevi(idelev);

alter table note
add foreign key (idelev) references elevi(idelev);

alter table note
add foreign key (idprof) references profesori(idprof);

alter table absente
change prezent absent bool;

alter table absente
change idnota idabsenta int not null auto_increment;

alter table absente
add foreign key (idelev) references elevi(idelev);

alter table absente
add foreign key (idprof) references profesori(idprof);

2.2 DML (Data Manipulation Language)

In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase.

Below you can find all the insert instructions that were created in the scope of this project:

insert into elevi (numeelev,clasa) values
('Ciobanu Alex',4),
('Roibu Ioana',3),
('Tanase Ion',2),
('Albu Radu',2),
('Popa Aura',1),
('Bodea Alina',1),
('Turcu Vasile',2),
('Florea Dana',4),
('Rosu George',3),
('Costea Angela',2);

insert into elevi (numeelev,clasa) values
('Ignat Raluca',4),
('Lavric Sorin',3),
('Manea Paul',1),
('Lupu Cristian',2);

insert into elevi (numeelev,clasa) values
('Toader Victor',1);

insert into profesori (numeprof,materie) values
('Costea Ion','informatica'),
('Popescu Dan','matematica'),
('Moraru Ana','lb romana'),
('Popa Ioana','lb engleza'),
('Vasilescu Andrei','desen'),
('Ionescu Emil','sport'),
('Bunea George','lb franceza'),
('Sobaru Alexia','muzica');

insert into profesori (numeprof,materie) values
('Roibu Costel','lb germana');

insert into parinti (numeparinte,idelev) values
('Ciobanu Alina',1),
('Ciobanu Dorel',1),
('Roibu Costel',2),
('Tanase Laura',3),
('Albu Rodica',4),
('Albu Florin',4),
('Popa Doina',5),
('Popa Dan',5),
('Bodea Iulian',6),
('Turcu Maria',7),
('Turcu Iosif',7),
('Florea Cezar',8),
('Rosu Horia',9),
('Rosu Ilinca',9),
('Costea Paula',10);

insert into parinti (numeparinte,idelev) values
('Ignat Ioan',11),
('Ignat Irina',11),
('Lavric Aurel ',12),
('Manea Elena',13),
('Lupu Vasile',14);

insert into note (ziua,idelev,idprof,materie,nota) values
('2024-01-22',1,2,'matematica',7),
('2024-01-28',1,1,'informatica',8),
('2024-02-14',1,3,'lb romana',10),
('2024-01-18',2,4,'lb engleza',9),
('2024-03-10',2,5,'desen',10),
('2024-03-11',3,6,'sport',9),
('2024-01-18',4,7,'lb franceza',7),
('2024-02-22',5,8,'muzica',10),
('2024-04-01',6,2,'matematica',5),
('2024-05-20',7,5,'desen',7),
('2024-05-02',8,8,'muzica',10),
('2024-04-12',9,7,'lb franceza',9),
('2024-01-19',10,3,'lb romana',6),
('2024-02-22',10,2,'matematica',4);

insert into note (ziua,idelev,idprof,materie,nota) values
('2024-06-12',14,2,'matematica',7);

insert into absente (ziua,idelev,idprof,materie,absent) values
('2024-02-21',2,2,'matematica',true),
('2024-02-20',1,1,'informatica',true),
('2024-03-11',1,3,'lb romana',true),
('2024-02-18',2,4,'lb engleza',true),
('2024-03-10',3,5,'desen',true),
('2024-04-11',3,6,'sport',true),
('2024-02-18',4,7,'lb franceza',true),
('2024-03-22',5,8,'muzica',true),
('2024-04-06',6,2,'matematica',true),
('2024-04-14',7,5,'desen',true),
('2024-05-22',8,8,'muzica',true),
('2024-06-02',9,6,'sport',true),
('2024-06-12',9,7,'lb franceza',true),
('2024-01-15',10,3,'lb romana',true),
('2024-03-11',10,6,'sport',true),
('2024-02-09',10,2,'matematica',true);

After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:

update absente 
set ziua='2024-03-19' 
where idabsenta=15;

2.3. DQL (Data Query Language)

After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean:

delete from profesori
where idprof between 10 and 16;

In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

#### afisati numele elevilor care sunt in clasa a patra
select numeelev from elevi where clasa=4;

#### afisati numele parintilor primului elev
select numeparinte from parinti where idelev=1;

#### afisati numele profesorilor si materiile predate
select numeprof,materie from profesori;

#### afisati numele profesorilor care predau diferite limbi si materia predata
select numeprof,materie from profesori where materie like 'lb%';

#### afisati toate notele la desen si muzica
select nota from note where materie='desen'or materie='muzica';

#### calculati media notelor la materia matematica
select avg(nota) from note where materie='matematica';

#### afisati notele mai mici decat 7 impreuna cu materia si id-ul elevului
select idelev,materie,nota from note where nota<7;

#### afisati cate note de 10 au fost puse in luna februarie 2024
select count(*) from note where nota=10
and ziua between '2024-02-01' and '2024-02-29';

#### afisati id-ul elevilor si materiile la care se inregistreaza absente in luna aprilie 2024
select idelev,materie from absente 
where ziua between '2024-04-01' and '2024-04-30';

#### afisati cate absente s-au inregistrat in luna iunie 2024
select count(*) from absente where ziua between '2024-06-01' and '2024-06-30';

#### afisati profesorii care sunt si parinti
select parinti.numeparinte
from parinti inner join profesori
on parinti.numeparinte=profesori.numeprof;

#### afisati datele in care s-au inregistrat si note si absente
select note.ziua
from note inner join absente
on note.ziua=absente.ziua;

Link fisier SQL [Git repo screenshot](https://github.com/armandaskalu/SQL-Database-afterschool/blob/main/afterschool.sql)
