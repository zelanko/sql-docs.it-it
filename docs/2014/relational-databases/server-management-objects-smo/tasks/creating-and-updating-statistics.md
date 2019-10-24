---
title: Creazione e aggiornamento delle statistiche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54995cc99aae2065112cbb510203b656c409dcac
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782132"
---
# <a name="creating-and-updating-statistics"></a>Creazione e aggiornamento delle statistiche
  In SMO le informazioni statistiche sull'elaborazione di query nel database possono essere raccolte tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Statistic>.  
  
 È possibile creare statistiche per qualsiasi colonna tramite gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>. Il metodo <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> può essere eseguito per aggiornare le statistiche nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Statistic>. I risultati possono essere visualizzati in Query Optimizer.  
  
## <a name="example"></a>Esempio  
 Per usare qualsiasi esempio di codice fornito, è necessario scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione per la creazione dell'applicazione. Per ulteriori informazioni, vedere [creare un Visual Basic progetto SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [creare un progetto Visual&#35; C SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-and-update-statistics-in-visual-basic"></a>Creazione e aggiornamento di statistiche in Visual Basic  
 In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStatistics1](SMO How to#SMO_VBStatistics1)]  -->  
  
## <a name="creating-and-update-statistics-in-visual-c"></a>Creazione e aggiornamento di statistiche in Visual C#  
 In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Reference the CreditCard table.   
  
           Table tb = db.Tables["CreditCard", "Sales"];  
            //Define a Statistic object by supplying the parent table and name   
            //arguments in the constructor.   
            Statistic stat = default(Statistic);  
            stat = new Statistic(tb, "Test_Statistics");  
            //Define a StatisticColumn object variable for the CardType column   
            //and add to the Statistic object variable.   
            StatisticColumn statcol = default(StatisticColumn);  
            statcol = new StatisticColumn(stat, "CardType");  
            stat.StatisticColumns.Add(statcol);  
            //Create the statistic counter on the instance of SQL Server.   
            stat.Create();  
        }  
```  
  
## <a name="creating-and-update-statistics-in-powershell"></a>Creazione e aggiornamento di statistiche in PowerShell  
 In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.  
  
```powershell
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks2012\tables  
  
#Get a reference to the table  
$tb = get-item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -argumentlist $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -argumentlist $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index   
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -argumentlist $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
