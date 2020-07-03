---
title: Utilizzo di filegroup e file per archiviare i dati | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 583c51578b2564b65580b8f82913d7974e7848d8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892405"
---
# <a name="using-filegroups-and-files-to-store-data"></a>Utilizzo di filegroup e file per archiviare dati
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  I file di dati vengono utilizzati per archiviare file di database. I file di dati vengono suddivisi in filegroup. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> dispone di una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> che fa riferimento a un oggetto <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection>. Ogni oggetto <xref:Microsoft.SqlServer.Management.Smo.FileGroup> di quella raccolta dispone di una proprietà <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A>. Questa proprietà fa riferimento a una raccolta <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> che contiene tutti i file di dati che appartengono al database. Un filegroup viene utilizzato principalmente per raggruppare file utilizzati per archiviare un oggetto di database. È opportuno distribuire un oggetto di database su diversi file poiché questa operazione può migliorare le prestazioni, specialmente se i file sono archiviati su unità disco diverse.  
  
 Ogni database creato automaticamente dispone di un filegroup denominato "Primary" e di un file di dati con lo stesso nome del database. È possibile aggiungere file e gruppi supplementari alle raccolte.  
  
## <a name="examples"></a>Esempi  
 Per gli esempi di codice seguenti, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Aggiunta di filegroup e file di dati a un database in Visual Basic  
 Il file di dati e il filegroup primari vengono creati automaticamente con i valori delle proprietà predefiniti. Nell'esempio di codice vengono specificati alcuni valori delle proprietà che è possibile utilizzare. In caso contrario, vengono utilizzati i valori delle proprietà predefiniti.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a FileGroup object called SECONDARY on the database.
Dim fg1 As FileGroup
fg1 = New FileGroup(db, "SECONDARY")
'Call the Create method to create the file group on the instance of SQL Server.
fg1.Create()
'Define a DataFile object on the file group and set the FileName property.
Dim df1 As DataFile
df1 = New DataFile(fg1, "datafile1")
df1.FileName = "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\datafile2.ndf"
'Call the Create method to create the data file on the instance of SQL Server.
df1.Create()
```
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Aggiunta di filegroup e file di dati a un database in Visual C#  
 Il file di dati e il filegroup primari vengono creati automaticamente con i valori delle proprietà predefiniti. Nell'esempio di codice vengono specificati alcuni valori delle proprietà che è possibile utilizzare. In caso contrario, vengono utilizzati i valori delle proprietà predefiniti.  
  
```  
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>Aggiunta di filegroup e file di dati a un database in PowerShell  
 Il file di dati e il filegroup primari vengono creati automaticamente con i valori delle proprietà predefiniti. Nell'esempio di codice vengono specificati alcuni valori delle proprietà che è possibile utilizzare. In caso contrario, vengono utilizzati i valori delle proprietà predefiniti.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Creazione, modifica e rimozione di un file di log in Visual Basic  
 Nell'esempio di codice viene creato un oggetto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, viene modificata una delle proprietà, quindi l'oggetto viene rimosso dal database.  
  
```vbnet  
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a LogFile object and set the database, name, and file name properties in the constructor.
Dim lf1 As LogFile
lf1 = New LogFile(db, "logfile1", "c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\logfile1.ldf")
'Set the file growth to 6%.
lf1.GrowthType = FileGrowthType.Percent
lf1.Growth = 6
'Run the Create method to create the log file on the instance of SQL Server.
lf1.Create()
'Alter the growth percentage.
lf1.Growth = 7
lf1.Alter()
'Remove the log file.
lf1.Drop()
```
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Creazione, modifica e rimozione di un file di log in Visual C#  
 Nell'esempio di codice viene creato un oggetto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, viene modificata una delle proprietà, quindi l'oggetto viene rimosso dal database.  
  
```  
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.   
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.   
            lf1.Drop();  
  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>Creazione, modifica e rimozione di un file di log in PowerShell  
 Nell'esempio di codice viene creato un oggetto <xref:Microsoft.SqlServer.Management.Smo.LogFile>, viene modificata una delle proprietà, quindi l'oggetto viene rimosso dal database.  
  
```powershell  
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [Filegroup e file di database](../../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
