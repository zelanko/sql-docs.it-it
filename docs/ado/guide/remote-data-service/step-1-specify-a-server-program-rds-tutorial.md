---
description: 'Passaggio 1: Specificare un programma del server (esercitazione su RDS)'
title: 'Passaggio 1: specificare un programma server (esercitazione su RDS) | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b5c76aebd80ff4a5706c9226abc051c03940707
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451953"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Passaggio 1: Specificare un programma del server (esercitazione su RDS)
Nel caso più generale, utilizzare [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oggetto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) metodo per specificare il programma server predefinito, [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)o il proprio programma server personalizzato (oggetto business). Viene creata un'istanza di un programma server nel server e viene restituito un riferimento al programma server o al *proxy*.  
  
 In questa esercitazione viene usato il programma server predefinito:  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio 2: richiamare il programma del server (esercitazione su RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Esercitazione su RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
