---
title: "Passaggio 1: Specificare un'applicazione Server (esercitazione su RDS) | Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6cecddfe127bba43852412b6d804254f35103def
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922110"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Passaggio 1: Specificare un programma del server (esercitazione su RDS)
Nel caso più generale, usare il [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetti [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) metodo per specificare il programma, server predefinito [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), o un'applicazione server personalizzata (oggetto business). Viene creata un'istanza di un programma server sul server e un riferimento all'applicazione server, oppure *proxy*, viene restituito.  
  
 Questa esercitazione Usa il programma server predefinito:  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 2: Richiamare il programma di Server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
