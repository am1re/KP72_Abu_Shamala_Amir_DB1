# KP72_Abu_Shamala_Amir_DB1

Лабораторна робота № 1.

Ознайомлення з базовими операціями СУБД PostgreSQL

КП-72 Абу Шамала Амір Махер

Варіант 1 - Страхова компанія (автомобілі)

Сутності:

Людина (Person)
CREATE TABLE public.person
(
    "person-id" integer NOT NULL GENERATED ALWAYS AS IDENTITY ( INCREMENT 1 START 1 MINVALUE 1 MAXVALUE 2147483647 CACHE 1 ),
    address text COLLATE pg_catalog."default",
    name text COLLATE pg_catalog."default" NOT NULL,
    phone text COLLATE pg_catalog."default",
    car integer,
    CONSTRAINT person_pkey PRIMARY KEY ("person-id"),
    CONSTRAINT car FOREIGN KEY (car)
        REFERENCES public.car ("VIN") MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

Автомобіль (Car)
CREATE TABLE public.car
(
    "VIN" integer NOT NULL,
    "Model" text COLLATE pg_catalog."default" NOT NULL,
    "Year" integer NOT NULL,
    CONSTRAINT car_pkey PRIMARY KEY ("VIN")
)

Випадок (Accident)
CREATE TABLE public.accident
(
    "record-number" integer NOT NULL,
    location text COLLATE pg_catalog."default" NOT NULL,
    date text COLLATE pg_catalog."default" NOT NULL,
    "damage-amount" text COLLATE pg_catalog."default" NOT NULL,
    person integer,
    CONSTRAINT accident_pkey PRIMARY KEY ("record-number"),
    CONSTRAINT person FOREIGN KEY (person)
        REFERENCES public.person ("person-id") MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)
