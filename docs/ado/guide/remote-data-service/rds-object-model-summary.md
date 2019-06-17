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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 434c27f5e2da0208ba5141664ccc69accfc2fbb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704233"
---
# <a name="rds-object-model-summary"></a>Riepilogo del modello a oggetti RDS
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Object|Descrizione|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Questo oggetto contiene un metodo per ottenere un server proxy. Il proxy può essere il valore predefinito o un'applicazione server personalizzata (oggetto business). Il programma del server può essere richiamato in Internet, intranet, una rete locale o da una libreria a collegamento dinamico locale.<br /><br /> Il **DataSpace** oggetto è sicuro per lo scripting.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Questo oggetto rappresenta il programma server predefinito. Esegue i servizi desktop remoto dati recupero e aggiornamento comportamento predefinito.<br /><br /> Il **DataFactory** oggetto non sicuro per lo script.|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Questo oggetto consente di richiamare automaticamente il **Servizi Desktop remoto. DataSpace** e **RDSServer** oggetti.<br /><br /> Usare questo oggetto per richiamare il comportamento di aggiornamento o il recupero dei dati di servizi desktop remoto predefinito.<br /><br /> Questo oggetto fornisce anche i mezzi per controlli visivi accedere restituito **Recordset** oggetto.<br /><br /> Il **DataControl** oggetto è sicuro per lo scripting.|  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS Scenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Esercitazione su RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Utilizzo e sicurezza per RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


