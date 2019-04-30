---
title: Gli oggetti di servizi desktop remoto | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- objects [ADO], RDS
- RDS objects [ADO]
ms.assetid: f2ac8b3b-f968-41c4-a504-7aee3538b7c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95a71e977f56932d28b9ca0382829d6a30c7b212
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042497"
---
# <a name="rds-objects"></a>Oggetti di Servizi Desktop remoto
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|||  
|-|-|  
|[DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Associa una query di data **Recordset** a uno o più controlli (ad esempio, una casella di testo, un controllo griglia o una casella combinata) per visualizzare i **Recordset** dati in una pagina Web.<br /><br /> Il **DataControl** oggetto è sicuro per lo scripting.|  
|[DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Implementa metodi che forniscono accesso ai dati di lettura/scrittura a specificate origini di dati per le applicazioni lato client.<br /><br /> Il **DataFactory** oggetto non sicuro per lo script.|  
|[DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|Crea proxy lato client di oggetti business personalizzata che si trova nel livello intermedio.<br /><br /> Il **DataSpace** oggetto è sicuro per lo scripting.|  
|[Interfaccia IRDSService (Servizi Desktop remoto)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)|Espone le [InvokeService (Servizi Desktop remoto)](../../../ado/reference/rds-api/invokeservice-rds.md) metodo, che viene utilizzato per restituire un puntatore all'interfaccia richiesta in una versione più con supporta dell'oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API di servizi desktop remoto](../../../ado/reference/rds-api/rds-api-reference.md)


