---
title: Modello di programmazione RDS con oggetti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2cfba2b659ed03f67d94c2c80812d7712e481f50
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704490"
---
# <a name="rds-programming-model-with-objects"></a>Modello di programmazione RDS con oggetti
L'obiettivo di servizi desktop remoto è per ottenere l'accesso a e aggiornare le origini dei dati tramite un intermediario, ad esempio IIS. Il modello di programmazione indica la sequenza di attività necessarie per portare a termine questo obiettivo. Il modello a oggetti specifica gli oggetti cui metodi e proprietà influiscono sul modello di programmazione.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Servizi Desktop remoto fornisce i mezzi per eseguire la sequenza di azioni seguente:  
  
-   Specificare il programma da richiamare sul server e ottenere un modo (proxy) per farvi riferimento dal client ([Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Richiamare il programma del server. Passare parametri all'applicazione server che identifica l'origine dati e il comando da eseguire (proxy o [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   L'applicazione server Ottiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto dall'origine dati, in genere utilizzando ADO. Facoltativamente, il **Recordset** oggetto viene elaborato nel server ([RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   Il programma del server restituisce l'elemento finale **Recordset** oggetto all'applicazione client (proxy).  
  
-   Sul client, il **Recordset** oggetto viene inserito in un form che può essere facilmente utilizzato dai controlli visual (controllo visivo e **Servizi Desktop remoto. DataControl**).  
  
-   Modifiche per il **Recordset** oggetto vengono inviati al server e consente di aggiornare l'origine dati (**Servizi Desktop remoto. DataControl** oppure **RDSServer**).  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo del modello a oggetti servizi desktop remoto](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace Object (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS Scenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


