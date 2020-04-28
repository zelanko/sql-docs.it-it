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
ms.openlocfilehash: 06bf7c811074ba70741fe77b06037f9f69c9cda4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922471"
---
# <a name="rds-programming-model-with-objects"></a>Modello di programmazione RDS con oggetti
L'obiettivo di Servizi Desktop remoto è ottenere l'accesso e aggiornare le origini dati tramite un intermediario come IIS. Il modello di programmazione specifica la sequenza di attività necessarie per portare a termine questo obiettivo. Il modello a oggetti specifica gli oggetti i cui metodi e proprietà influiscono sul modello di programmazione.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS fornisce i mezzi per eseguire la sequenza di azioni seguente:  
  
-   Specificare il programma da richiamare sul server e ottenere un metodo (proxy) per farvi riferimento dal client ([RDS). Spazio di DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Richiamare il programma server. Passare i parametri al programma server che identifica l'origine dati e il comando da emettere (proxy o [RDS). DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   Il programma server ottiene un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dall'origine dati, in genere tramite ADO. Facoltativamente, l'oggetto **Recordset** viene elaborato nel server ([RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   Il programma server restituisce l'oggetto **Recordset** finale all'applicazione client (proxy).  
  
-   Nel client, l'oggetto **Recordset** viene inserito in un modulo che può essere facilmente utilizzato dai controlli visivi (controllo visivo e Servizi Desktop remoto **. DataControl**).  
  
-   Le modifiche apportate all'oggetto **Recordset** vengono restituite al server e utilizzate per aggiornare l'origine dati (**RDS). DataControl** o **RDSServer. DataFactory**).  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo del modello a oggetti RDS](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [Oggetto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Oggetto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Scenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Oggetto recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


