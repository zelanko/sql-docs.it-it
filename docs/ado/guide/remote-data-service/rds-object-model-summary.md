---
title: Riepilogo del modello a oggetti RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 95ddd84bfd755e044d97a6043f295014933ae18c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763592"
---
# <a name="rds-object-model-summary"></a>Riepilogo del modello a oggetti RDS
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Oggetto|Descrizione|  
|------------|-----------------|  
|[RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Questo oggetto contiene un metodo per ottenere un proxy server. Il proxy può essere quello predefinito o un programma server personalizzato (oggetto business). Il programma server può essere richiamato su Internet, una rete Intranet, una rete locale o una libreria a collegamento dinamico locale.<br /><br /> L'oggetto **DataSpace** è sicuro per lo scripting.|  
|[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Questo oggetto rappresenta il programma server predefinito. Esegue il comportamento di aggiornamento e recupero dati RDS predefinito.<br /><br /> L'oggetto **DataFactory** non è sicuro per lo scripting.|  
|[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Questo oggetto può richiamare automaticamente il Servizi Desktop remoto **. Oggetti DataSpace** e **RDSServer. DataFactory** .<br /><br /> Utilizzare questo oggetto per richiamare il comportamento di aggiornamento o recupero dati RDS predefinito.<br /><br /> Questo oggetto fornisce inoltre i mezzi per i controlli visivi per accedere all'oggetto **Recordset** restituito.<br /><br /> L'oggetto **DataControl** è sicuro per lo scripting.|  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Scenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


