# Geographic Information Systems 2023-2024

# Exercise 1 - ArcGIS Pro  - Install and get familiar with the interface

## Introduction

In this exercise, you will set up your system to have a fully functional ArcGIS Pro ver. 3.2 installation.
You will also learn to identify the different components of the interface of the software and the workflow 
to manage data and perform analysis.

## 1. Install ArcGIS Pro ver 3.2

ArcGIS Pro is a proprietary software. In order to use it, you need to use a licence provided by ISA. This 
exercise will guide you through the several steps to install and set the licence.

The **System Requirements** are available at 
[https://pro.arcgis.com/en/pro-app/latest/get-started/arcgis-pro-system-requirements.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/arcgis-pro-system-requirements.htm). If your system operating system is a MacOS 
ou linux, you need to install a virtual machine with Windows 10 or above.

You can download the installation file from ISA CIISA service. In order to do 
this, your computer needs to be connected inside the ISA campus network (wifi 
eduroam). If you are outside the ISA network, you need establish a VPN connection 
(see instructions here: [https://www.isa.ulisboa.pt/di/servicos/acesso-vpn](https://www.isa.ulisboa.pt/di/servicos/acesso-vpn))

### **Step 1: Access the software repository @ISA**

Open a run panel in Windows with the following key combination: Windows key + R
Write the network path to the text box:
```
\\CIISAfs.isa.utl.loc\Apps\ESRI
```

Enter  your ISA login credentials, in the format:

username: `SIISA\isa1*****`

password: `*******`

### **Step 2: Copy installation and patch files to your computer**

Open the network folder `ArcGIS_Pro`, and copy the installation package file 
`ArcGISPro_303_184244.exe` to your computer.

### **Step 3: Run installation and patch files to your computer**
Run the downloaded file, accepting the default options. You will be prompted to 
use the most recent version 3.2. Accept that and do updates as suggested.


### **Step 4: Configure the licence**

Run ArcGIS Pro for the first time and activate the licence. 

- Click 
***Configure licensing***
- Select **Named User license**, and in options enter ArcGIS Online, with the URL `https://www.arcgis.com`. Click **OK**. (see image)

![License Panel](./images/ex01_img01.png)

- In the login panel, enter in organisation URL `ulisboa` and click continue. (see image)

![Insert server](./images/ex01_img02.png)

- Do your centralized authentication, using your **@edu.ulisboa.pt**. If you don't 
have that active, you need to activate it at [https://utilizador.ulisboa.pt/UlisboaUsers/home](https://utilizador.ulisboa.pt/UlisboaUsers/home).

### **Step 5: Offline use**

This is not authorized by the system administrator, meaning that you need to be 
connected to the internet in order to be able to use your ArcGIS installation.

### **Step 6 (Optional):  Create a free ArcGIS Online**

You can create a free ArcGIS Online Public account. This gives access to a large catalog of online data.
Go to [https://tinyurl.com/rfmm6nnn](https://tinyurl.com/rfmm6nnn) and provide the required information to register. 

Confirm the new account in your email to activate it.
When opening ArcGIS Pro, click on **Sign In** to login.

Do not forget to sign out, when closing the application, particularly if you are using a classroom or shared computer.

## 2. Get familiar with ArcGIS Pro 3.2 (tutorial)

### 2.1. Learn about the ArcGIS Pro interface

- Create a new project from a blank map template. Understand the interface, including menus (tabs), tools ribbon, view pane, contents pane, catalog pane, table pane.

- Verify that tabs, ribbon and panes are changed dynamically, depending on the tools and views selected.
Learn how to reset panes to the original configuration

Support material: [https://pro.arcgis.com/en/pro-app/latest/get-started/introducing-arcgis-pro.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/introducing-arcgis-pro.htm)


### 2.2. Create a map and add data

- Learn how to create a new project, a new map, and add data to the map.

- Understand the concepts and differences between projects, maps, (geo)databases, geopackages, data and features

Support material:

- [https://pro.arcgis.com/en/pro-app/latest/get-started/create-a-project.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/create-a-project.htm)

- [https://pro.arcgis.com/en/pro-app/latest/get-started/add-data-to-your-project.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/add-data-to-your-project.htm)

### 2.3. Other resources

ArcGIS Pro manual: [https://pro.arcgis.com/en/pro-app/latest/get-started/get-started.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/get-started.htm)

Other tutorials: [https://pro.arcgis.com/en/pro-app/latest/get-started/pro-quickstart-tutorials.htm](https://pro.arcgis.com/en/pro-app/latest/get-started/pro-quickstart-tutorials.htm)


### 2.4. Understand geodatabases 

**Geodatabases** are a collection of geographic datasets. They contain a series of tables to hold feature classes, raster datasets, attributes.

Data in geodatabases can be stored in database management systems (DBMS) or in the file system. ArcGIS supports different formats:

- **GeoPackage** - an open, standards-based, platform-independent, portable, self-describing, compact format for transferring geospatial information
- **File geodatabase** - ESRI proprietary format, file bases
**Personal geodatabase** - ESRI proprietary format, uses MS Access format
- **Enterprise geodatabase** - data is stored inside a database (IBM Db2, IBM Informix, Microsoft SQL Server, Oracle, PostgreSQL)

The use of geodatabases allow improved performance and consistency in the use of data. But its management should be done within the GIS software, to ensure consistency. Do not manage these files (copy, delete, duplicate, etc) with your file browser.

In ArcGIS Pro, the native (best supported) format for geodatabases are **File geodatabase**, **Personal geodatabase** and **Enterprise geodatabase**. We should use file geodatabases for our projects.

To ensure interoperability and future data preservation, final data outputs or layers to preserve should be stored in the standard geodatabase format **GeoPackage**.

