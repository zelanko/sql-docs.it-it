---
description: 'Passaggio 2: Richiamare il programma del server (esercitazione su RDS)'
title: 'Passaggio 2: richiamare il programma del server (esercitazione su RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b864578b67eda29c703bcf4952a9a2878aafe9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451943"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Passaggio 2: Richiamare il programma del server (esercitazione su RDS)
Quando si richiama un metodo sul *proxy*client, il programma effettivo sul server esegue il metodo. In questo passaggio verrà eseguita una query sul server.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Parte A** Se non si usa [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) in questa esercitazione, il modo più pratico per eseguire questo passaggio consiste nell'usare [RDS. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) . **RDS. DataControl** combina il passaggio precedente della creazione di un proxy, con questo passaggio, eseguendo la query.  
  
 Impostare **RDS. ** Proprietà del [Server](../../../ado/reference/rds-api/server-property-rds.md) oggetti DataControl per identificare la posizione in cui deve essere creata un'istanza del programma server. proprietà [Connect](../../../ado/reference/rds-api/connect-property-rds.md) per specificare la stringa di connessione per l'accesso all'origine dati. e la proprietà [SQL](../../../ado/reference/rds-api/sql-property.md) per specificare il testo del comando di query. Eseguire quindi il metodo [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md) per fare in modo che il programma server si connetta all'origine dati, recuperi le righe specificate dalla query e restituisca un oggetto **Recordset** al client.  
  
 Questa esercitazione non usa Servizi Desktop remoto **. DataControl**, ma questo è il modo in cui l'aspetto sarebbe stato:  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Né l'esercitazione richiama Servizi Desktop remoto con gli oggetti ADO, ma questo è il modo in cui verrebbe eseguita la ricerca:  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **Parte B** Il metodo generale per eseguire questo passaggio consiste nel richiamare il metodo di [query](../../../ado/reference/rds-api/query-method-rds.md) dell'oggetto **RDSServer. DataFactory** . Tale metodo accetta una stringa di connessione, che viene utilizzata per connettersi a un'origine dati e un testo del comando, utilizzato per specificare le righe che devono essere restituite dall'origine dati.  
  
 Questa esercitazione usa il metodo di **query** dell'oggetto **DataFactory** :  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 3: il server ottiene un recordset (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
