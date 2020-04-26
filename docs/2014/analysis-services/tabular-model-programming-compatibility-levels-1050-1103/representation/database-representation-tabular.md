---
title: Rappresentazione del database (tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 16a233fb-f83b-4ca1-acb5-6186eca0a62c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 377b85c22d1c6da9f5296d6ad57a86028e022785
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62757813"
---
# <a name="database-representationtabular"></a>Rappresentazione del database(tabulare)
  In modalità tabulare, il database è il contenitore per tutti gli oggetti del modello tabulare.  
  
## <a name="database-representation"></a>Rappresentazione di un database  
 Il database è il posto dove si trovano tutti gli oggetti che formano un modello tabulare. All'interno del database lo sviluppatore trova oggetti come connessioni, tabelle, ruoli e molti altri ancora.  
  
### <a name="database-in-amo"></a>Database in AMO  
 Quando si utilizza AMO (Analysis Management Objects) per gestire un database modello tabulare, l'oggetto <xref:Microsoft.AnalysisServices.Database> ha una corrispondenza uno-a-uno in AMO (Analysis Management Objects) con l'oggetto logico del database in un modello tabulare.  
  
> [!NOTE]  
>  Per accedere a un oggetto di database, in AMO (Analysis Management Objects) l'utente deve avere accesso a un oggetto server e connettersi.  
  
### <a name="database-in-adomdnet"></a>Database in ADOMD.Net  
 Quando si utilizza ADOMD per consultare ed eseguire una query su un database modello tabulare, la connessione a un database specifico si ottiene mediante l'oggetto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 È possibile connettersi direttamente a un determinato database utilizzando il seguente frammento di codice:  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
...  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
...  
  
```  
  
 Inoltre, tramite un oggetto connessione esistente (che non è stato chiuso) è possibile passare dal database corrente a un altro come mostrato nel seguente frammento di codice:  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>Database in AMO  
 Quando si utilizza AMO per gestire un oggetto di database, iniziare con un oggetto <xref:Microsoft.AnalysisServices.Server>. Quindi cercare il database nella raccolta di database oppure creare un nuovo database aggiungendone uno alla raccolta.  
  
 Nel frammento di codice seguente vengono illustrati i passaggi per connettersi a un server e creare un database vuoto, dopo aver verificato che il database non esista:  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 Per comprendere praticamente le modalità di utilizzo di AMO (Analysis Management Objects) per creare e modificare le rappresentazioni di database vedere il codice sorgente dell'esempio Tabular AMO 2012; in particolare controllare nel seguente file di origine: Database.cs. Il codice di esempio viene fornito solo come supporto ai concetti logici illustrati in questo argomento e non deve essere utilizzato in un ambiente di produzione.  
  
  
