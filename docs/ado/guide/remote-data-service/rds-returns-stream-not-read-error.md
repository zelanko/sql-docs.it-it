---
description: RDS restituisce un &quot; errore di lettura del flusso &quot;
title: RDS restituisce un &quot; errore di lettura del flusso &quot; | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 6acb603594acdd23f8ad8764c9b9a692acabdb9b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724902"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS restituisce un &quot; errore di lettura del flusso &quot;
"Impossibile leggere l'oggetto flusso perché è vuoto o la posizione corrente si trova alla fine del flusso. Per i flussi non vuoti, impostare la posizione corrente con la proprietà Position. Per determinare se un flusso è vuoto, controllare la proprietà Size ".  
  
 Se viene visualizzato questo messaggio di errore, è possibile che si sia tentato di usare una query gerarchica con parametri su http. RDS non consente di utilizzare gerarchie con parametri remoti.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](/dotnet/framework/wcf/).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](./rds-fundamentals.md)