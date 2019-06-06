---
title: "Passaggio 5: L'oggetto DataControl viene reso utilizzabile (esercitazione su RDS) | Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f654bc1ccd913c5fc31f81cae67ffdb84e80f952
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704158"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>Passaggio 5: L'oggetto DataControl viene reso utilizzabile (esercitazione su RDS)
L'oggetto restituito **Recordset** l'oggetto è disponibile per l'uso. È possibile esaminare, esplorare o modificarlo come qualsiasi altra **Recordset**. Operazioni eseguibili con il **Recordset** dipende dall'ambiente. Visual Basic e Visual C++ sono controlli visivi che è possono usare una **Recordset** direttamente o indirettamente con l'ausilio di un controllo dei dati di attivazione.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Ad esempio, se si visualizzano una pagina Web in Microsoft Internet Explorer, è possibile visualizzare il **Recordset** dati in un controllo visivo dell'oggetto. Non è possibile accedere ai controlli visivi in una pagina Web una **Recordset** direttamente l'oggetto. Tuttavia, essi possono accedere i **Recordset** dell'oggetto tramite il [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md). Il **Servizi Desktop remoto. DataControl** diventa utilizzabile da un oggetto visivo controllare quando relativo [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) viene impostata il **Recordset** oggetto.  
  
 L'oggetto controllo visivo deve avere relativi **DATASRC** parametro impostato sul **Servizi Desktop remoto. DataControl**e la relativa **DATAFLD** impostata su un **Recordset** campo dell'oggetto (colonna).  
  
 In questa esercitazione, impostare il **SourceRecordset** proprietà:  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 6: Le modifiche vengono inviate al Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
