---
title: Uso di filegroup e file per dati Store | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: efeb2de880834723f37755a47618ece97d31af65
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270751"
---
# <a name="using-filegroups-and-files-to-store-data"></a>Utilizzo di filegroup e file per archiviare dati
  I file di dati vengono utilizzati per archiviare file di database. I file di dati vengono suddivisi in filegroup. L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Database> dispone di una proprietà <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> che fa riferimento a un oggetto <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection>. Ogni oggetto <xref:Microsoft.SqlServer.Management.Smo.FileGroup> di quella raccolta dispone di una proprietà <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A>. Questa proprietà fa riferimento a una raccolta <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> che contiene tutti i file di dati che appartengono al database. Un filegroup viene utilizzato principalmente per raggruppare file utilizzati per archiviare un oggetto di database. È opportuno distribuire un oggetto di database su diversi file poiché questa operazione può migliorare le prestazioni, specialmente se i file sono archiviati su unità disco diverse.  
  
 Ogni database creato automaticamente dispone di un filegroup denominato "Primary" e di un file di dati con lo stesso nome del database. È possibile aggiungere file e gruppi supplementari alle raccolte.  
  
## <a name="examples"></a>Esempi  
 Per gli esempi di codice seguenti, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Aggiunta di filegroup e file di dati a un database in Visual Basic  
 Il file di dati e il filegroup primari vengono creati automaticamente con i valori delle proprietà predefiniti. Nell'esempio di codice vengono specificati alcuni valori delle proprietà che è possibile utilizzare. In caso contrario, vengono utilizzati i valori delle proprietà predefiniti.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
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
  
```  
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
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
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
  
```  
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
 [Filegroup e file di database](../../databases/database-files-and-filegroups.md)  
  
  
