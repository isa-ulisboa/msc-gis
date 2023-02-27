# Geographic Information Systems 2022-2023

# Exercise 4 - Organising geographic data

## Introduction

This exercise will use a dataset made available by the Lisbon City Council open data initiative. This corresponds to the with the location of trees in streets and public spaces in the 
city of Lisbon.


The goals of these exercise are:

> - Organise a dataset according to the rules of the Normal Forms (NF)
> - Create joins between geographic datasets and tables and visualize in your GIS

**What do you need:**

The geographic dataset is available on the 
[Lisboa Aberta](https://lisboaaberta.cm-lisboa.pt/index.php/pt/dados/conjuntos-de-dados) 
platform.

In the platform, if you make a search for the keyword `arvoredo`, this will lead to a first result with metadata about the resource. To download as `csv`, you can click on the link [http://geodados.cm-lisboa.pt/datasets/arvoredo](http://geodados.cm-lisboa.pt/datasets/arvoredo). 


For this exercise, we are making available two versions of the dataset in csv format, in portuguese and in english, to easier understanding of the data. These files were also cleaned for data inconsistencies:

- Portuguese: [descarregar dados]()
- English: [download data]()

The downloaded table contains the following columns:

| Column	| Description | 
|----|----|
|X	|Longitude coordinate, in geographic format, in WGS84 reference system|
|Y	|Latitude coordinate, in geographic format, in WGS84 reference system|
|OBJECTID	|Unique identifier of the geographic feature|
|COD_SIG_NEW	|Other unique identifier of the geographic feature|
|MORADA	|Address of the location of the tree|
|ESPECIE_VA	|Scientific name of the tree species|
|PAP	|circumference at chest height|
|MANUTENCAO	|Entiy responsible for the maintenance|
|OCUPACAO	|type of occupation|
|LOCAL	|type of place|
|TIPOLOGIA	|type of implantation of the tree|
|FREG_2012	|Name of the freguesia|
|NOME_VULGA	|common name of the tree|
|GlobalID	|global unique identifier|

## Task 01 - transform the dataset to a normalised format, according to the 3rd normal form

Your first task is to create a 3rd NF dataset from the provided csv file. We suggest the following path to achieve that goal:

### Step 1 - analyse you problem and create a diagram
You should study and plan for the transformations required:
- analyse the original table to identify the different entities that might be present in the original table
- identify the new tables that need to be created for the identified entities, in order to solve partial or transitive dependencies
- write down a text representation of the new table schemas, identifying the primary key. Rewrite the schema the original table, replacing, when applicable, the original column by the corresponding foreign key

### Step 2 - perform data transformations
Once you're confident with the solution achieved, make data transformations:
- create a new table for each of these entities, removing duplicate rows
    - you can use pivot tables or data filters of your spreadsheet software. The specific method depends if your're using Excel, Libreoffice or OpenOffice, Google Sheets, MacOS Numbers or other.
    - you can also use [OpenRefine](https://openrefine.org/) for this purpose
- add unique identifiers to each of the new tables. This can be simple a sequential integer number
- add a new column in the original table to contain the IDs that you created for each of the new tables. These will be foreign keys.
- use `VLOOKUP` function of your spreadsheet software to fill in these columns with the unique identifiers.
- make IDs permanent with a copy --> paste as values action
- delete the column of the parameter that is replaced by its ID.



