---
description: Oggetti di Servizi Desktop remoto
title: Oggetti RDS | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 477db26b27b0b6222da55585661db1dc37d64b82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438783"
---
# <a name="rds-objects"></a>Oggetti di Servizi Desktop remoto
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Oggetto|Descrizione|  
|-|-|  
|[DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Associa un **Recordset** di query di dati a uno o più controlli, ad esempio una casella di testo, un controllo griglia o una casella combinata, per visualizzare i dati del **Recordset** in una pagina Web.<br /><br /> L'oggetto **DataControl** è sicuro per lo scripting.|  
|[DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Implementa metodi che forniscono accesso ai dati in lettura/scrittura alle origini dati specificate per le applicazioni lato client.<br /><br /> L'oggetto **DataFactory** non è sicuro per lo scripting.|  
|[Spazio di DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|Crea proxy sul lato client per oggetti business personalizzati che si trovano nel livello intermedio.<br /><br /> L'oggetto **DataSpace** è sicuro per lo scripting.|  
|[Interfaccia IRDSService (Servizi Desktop remoto)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)|Espone il metodo [InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md) , utilizzato per restituire un puntatore all'interfaccia richiesta su una versione più idonea dell'oggetto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento per l'API RDS](../../../ado/reference/rds-api/rds-api-reference.md)


