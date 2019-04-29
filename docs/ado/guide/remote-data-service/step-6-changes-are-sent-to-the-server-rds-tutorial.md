---
title: 'Passaggio 6: Le modifiche vengono inviate al Server (esercitazione su RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bfeb9ad607fc35c055e025fcc67435323d3143e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955718"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>Passaggio 6: Le modifiche vengono inviate al server (esercitazione su RDS)
Se il **Recordset** che l'oggetto viene modificato, eventuali modifiche (vale a dire, le righe che vengono aggiunte, modificate o eliminate) possono essere inviate al server.  
  
> [!NOTE]
>  Il comportamento predefinito di servizi desktop remoto può essere richiamato in modo implicito con gli oggetti ADO e il Provider .NET Remoting Microsoft OLE DB. Le query possono restituire **Recordset**s e modificati **Recordset**s può aggiornare l'origine dati. Questa esercitazione non richiama Servizi Desktop remoto con gli oggetti ADO, ma è come se fosse ha sempre fatto:  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **La parte** Assume per questo caso in cui è stato usato solo il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e che un **Recordset** oggetto è associato a questo punto il **Servizi Desktop remoto. DataControl**. Il [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) metodo aggiorna l'origine dati con le modifiche per il **Recordset** oggetto se la [Server](../../../ado/reference/rds-api/server-property-rds.md) e [Connect](../../../ado/reference/rds-api/connect-property-rds.md) le proprietà sono ancora impostate.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **La parte B** in alternativa, è possibile aggiornare il server con il [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) oggetto specificando una connessione e un' **Recordset** oggetto.  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **Questa è la fine dell'esercitazione.**  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Provider di servizi remoti Microsoft OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
