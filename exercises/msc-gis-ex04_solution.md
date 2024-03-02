<style type="text/css">
  .doubleUnderline {
    border-bottom: 3px double #000;
  }
</style>


# Geographic Information Systems 2023-2024

# Exercise 4 - Organizing geographic data - Solution

**QUESTION 1:** provide the table schema in text notation for all the tables that 
you identified or created

Double underline: *primary key*
single underline: *foreign key*


> ARVOREDO_NORM(X,Y,<span class="doubleUnderline">OBJECTID</span>,COD_SIG_NEW,<u>morada_ID</u>,<u>especie_ID</u>,PAP,<u>manutencao_ID</u>,<u>ocupacao_ID</u>,<u>local_tipo_ID</u>,<u>tipologia_ID</u>,GlobalID)<br>
> ESPECIE_VA(<span class="doubleUnderline">especie_ID</span>,ESPECIE_VA,NOME_VULGAR)<br>
> MORADA(<span class="doubleUnderline">morada_ID</span>,MORADA,FREG_2012)<br>
> LOCAL_TIPO(<span class="doubleUnderline">local_tipo_ID</span>,LOCAL)<br>
> MANUTENCAO(<span class="doubleUnderline">manutencao_ID</span>,MANUTENCAO)<br>
> TIPOLOGIA(<span class="doubleUnderline">tipologia_ID</span>,TIPOLOGIA)


**QUESTION 2:** Include in the report screenshots of the first ten rows of each 
table you created. The names of the columns should be visible and correspond to 
the text schema included in Question 1.

**arvoredo_norm**

![arvoredo_norm](images/ex04_img01.jpg)

**especie_va**

<img src="images/ex04_img02.jpg" height="100">

**morada**

<img src="images/ex04_img03.jpg" height="100">

**local_tipo**

<img src="images/ex04_img04.jpg" height="100">

**manutencao**

<img src="images/ex04_img05.jpg" height="100">

**ocupacao**

<img src="images/ex04_img06.jpg" height="100">

**tipologia**

<img src="images/ex04_img07.jpg" height="100">


**QUESTION 3**: 
How many trees with type of implantation `Canteiro` exists in freguesia `ALCÂNTARA`?
Describe how did you determined it?

There are 133 trees in freguesia *Alcântara* with the implantation of type *canteiro*.

The following steps were follow to achieve the solution:

1. Add all csv tables to GIS project.
2. Table `arvoredo_norm` is added as a text file with point geometry, where `x` are longitudes and `y` latitides.
3. Create table joins between `arvoredo_norm` and each of the tables, setting the primay key and foreign key of each table as defined in question 01 
4. Add `CAOP` layer
5. Make a spatial join operation between `arvoredo_norm` and `CAOP`, to add the name of freguesia to the attribute table of the first table. This is necessary to avoid possible errors in naming of the freguesia in the original table.
6. Make a selection by attribute on the table `arvoredo_norm`, based on the name of freguesia, with the value `ALCÂNTARA`. Determine the number of selected features.