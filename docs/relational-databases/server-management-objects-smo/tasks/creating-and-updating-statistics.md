---
title: Creazione e aggiornamento delle statistiche
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: seo-dt-2019
ms.date: 06/04/2020
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c3e04a1e6434c0319d4797460c6574d2fc81a973
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779103"
---
# <a name="create-and-update-statistics"></a>Creazione e aggiornamento delle statistiche

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

In SMO le informazioni statistiche sull'elaborazione di query nel database possono essere raccolte tramite l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Statistic>.

È possibile creare statistiche per qualsiasi colonna usando l' <xref:Microsoft.SqlServer.Management.Smo.Statistic> <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> oggetto e. Il metodo <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> può essere eseguito per aggiornare le statistiche nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Statistic>. I risultati possono essere visualizzati in Query Optimizer.

## <a name="example"></a>Esempio

Per utilizzare qualsiasi esempio di codice fornito, è possibile scegliere l'ambiente di programmazione, il modello di programmazione e il linguaggio di programmazione in cui creare l'applicazione. Per altre informazioni, vedere [creare un progetto Visual C&#35; SMO in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).

## <a name="create-and-update-statistics-in-visual-basic"></a>Creazione e aggiornamento di statistiche in Visual Basic

In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```vb
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Reference the CreditCard table.
Dim tb As Table
tb = db.Tables("CreditCard", "Sales")
'Define a Statistic object by supplying the parent table and name arguments in the constructor.
Dim stat As Statistic
stat = New Statistic(tb, "Test_Statistics")
'Define a StatisticColumn object variable for the CardType column and add to the Statistic object variable.
Dim statcol As StatisticColumn
statcol = New StatisticColumn(stat, "CardType")
stat.StatisticColumns.Add(statcol)
'Create the statistic counter on the instance of SQL Server.
stat.Create()
```

## <a name="create-and-update-statistics-in-c"></a>Creazione e aggiornamento di statistiche in C #

In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```csharp
public static void CreatingAndUpdatingStatistics()
{
    // Connect to the local, default instance of SQL Server.
    var srv = new Server();

    // Reference the AdventureWorks2012 database.
    var db = srv.Databases["AdventureWorks"];

    // Reference the CreditCard table.
    var tb = db.Tables["CreditCard", "Sales"];

    // Define a Statistic object by supplying the parent table and name
    // arguments in the constructor.
    var stat = new Statistic(tb, "Test_Statistics");

    // Define a StatisticColumn object variable for the CardType column
    // and add to the Statistic object variable.
    var statcol = new StatisticColumn(stat, "CardType");
    stat.StatisticColumns.Add(statcol);

    //Create the statistic counter on the instance of SQL Server.
    stat.Create();

    // List all the statistics object on the table (you will see the newly created one)
    foreach (var s in tb.Statistics.Cast<Statistic>())
        Console.WriteLine($"{s.ID}\t{s.Name}");

    // Output:
    //  2       AK_CreditCard_CardNumber
    //  1       PK_CreditCard_CreditCardID
    //  3       Test_Statistics
 }
```

## <a name="create-and-update-statistics-in-powershell"></a>Creare e aggiornare le statistiche in PowerShell

In questo esempio di codice viene creata una nuova tabella in un database esistente per il quale vengono creati gli oggetti <xref:Microsoft.SqlServer.Management.Smo.Statistic> e <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn>.

```powershell
Import-Module SQLServer

# Connect to the local, default instance of SQL Server.  
$srv = Get-Item SQLSERVER:\SQL\localhost\DEFAULT

# Reference the AdventureWorks database.
$db = $srv.Databases["AdventureWorks"]

# Reference the CreditCard table.
$tb = $db.Tables["CreditCard", "Sales"]

# Define a Statistic object by supplying the parent table and name
# arguments in the constructor.
$stat = New-Object Microsoft.SqlServer.Management.Smo.Statistic($tb, "Test_Statistics")

# Define a StatisticColumn object variable for the CardType column
# and add to the Statistic object variable.
$statcol = New-Object Microsoft.SqlServer.Management.Smo.StatisticColumn($stat, "CardType")
$stat.StatisticColumns.Add($statcol)

# Create the statistic counter on the instance of SQL Server.
$stat.Create()

# Finally dump all the statistics (you can see the newly created one at the bottom)
$tb.Statistics

# Output:
# Name                                Last Updated Is From Index  Statistic Columns
#                                                  Creation
# ----                                ------------ -------------- -----------------
# AK_CreditCard_CardNumber      10/27/2017 2:33 PM True           {CardNumber}
# PK_CreditCard_CreditCardID    10/27/2017 2:33 PM True           {CreditCardID}
# Test_Statistics                 6/4/2020 8:11 PM False          {CardType}
```
