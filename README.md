# sistema de registro de empregador-trabalhador
Um programa de contabilidade que contém informações de funcionários e empregadores e registros de relacionamentos entre eles.

---
## Screenshot
<p align="center"><strong>Login</strong></p>
<p align="center"><img src="https://user-images.githubusercontent.com/71611710/157845415-c8f293df-5e1a-4ac5-a066-1971ee3ab6ae.png"></p>

| **Homepage**            | **Employer registration**|  **Worker registration**
:------------------------:|:------------------------:|:-------------------------:
![2-home_page](https://user-images.githubusercontent.com/71611710/157845986-0b99502d-ec6a-411c-999c-d37859dcf47e.png) | ![3-new_employer](https://user-images.githubusercontent.com/71611710/157849241-2a4ea23f-f195-4152-ab57-b2da20a1ea87.png)  |  ![3-new_worker](https://user-images.githubusercontent.com/71611710/157849850-5c6cfda1-05cd-4164-8287-474496cd189e.png)

| **Search Box**  | **Registration document**
:----------------:|:-------------------------:
![5-view_worker](https://user-images.githubusercontent.com/71611710/157850829-c03944a1-bd1b-41d6-875b-61f8d8ce4d62.png) | ![7-new_record_optionpane](https://user-images.githubusercontent.com/71611710/158039292-30c103d1-bdaa-4f3f-bd36-342815fd6efd.png)

---

## Requirements
Postgresql é usado neste programa. Você pode encontrar o arquivo jar necessário para a conexão java postgresql aqui:

> https://jdbc.postgresql.org/download.html

Ou você pode usar um banco de dados diferente, mas para que isso funcione, altere:
```
DriverManager.getConnection("jdbc:database://host:port/database-name", "user-name", "password");
```
for postgresql:
```
DriverManager.getConnection("jdbc:postgresql://localhost:5432/db", "postgres", "password");
```
---

**E, finalmente, para não obter um erro de banco de dados, você deve adicionar as seguintes tabelas ao banco de dados:**
```
CREATE TABLE admin(id smallserial primary key not null, username varchar, password varchar);
CREATE TABLE employer(employer_id serial primary key not null, name varchar not null, surname varchar not null, business varchar, phonenumber varchar);
CREATE TABLE employer(employer_id serial primary key not null, name varchar not null, surname varchar not null, business varchar, phonenumber varchar);
CREATE TABLE worker(worker_id serial primary key not null, name varchar not null, surname varchar not null, phone_number varchar);
CREATE TABLE worker_record(worker_record_id serial primary key not null, worker_id integer references worker(worker_id), employer_id integer references employer(employer_id), date varchar(10) not null, wage smallint not null);
CREATE TABLE employer_record(employer_record_id serial primary key not null, employer_id integer references employer(employer_id), date varchar(10) not null, note varchar(255), number_worker smallint not null, wage smallint not null);
CREATE TABLE worker_payment(worker_payment_id serial primary key not null, worker_id integer references worker(worker_id), employer_id integer references employer(employer_id), date varchar(10), not null, paid integer not null);
CREATE TABLE employer_payment(employer_payment_id serial primary key not null, employer_id integer references employer(employer_id), date varchar(10) not null, paid integer not null);
```

