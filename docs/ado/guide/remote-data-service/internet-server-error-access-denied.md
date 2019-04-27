---
title: 'Errore del server Internet: Accesso negato | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b7c562e57341dd027a4cd9bdc3a0fa4bbe51ae5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634382"
---
# <a name="internet-server-error-access-denied"></a>Errore del server Internet: Accesso negato
Se si verifica questo errore, in genere significa che Microsoft Internet Information Services (IIS) ha restituito lo stato seguente:  
  
 HTTP_STATUS_DENIED 401  
  
 Assicurarsi che le directory a cui accede IIS hanno le autorizzazioni appropriate. Servizi Desktop remoto può comunicare con un server Web IIS in esecuzione in una delle tre modalità di autenticazione della Password: Anonymous, Basic o NT Challenge/Response (chiamata autenticazione Windows integrata in Windows 2000). Inoltre, il server Web deve avere autorizzazioni per il computer di origine dati se si tratta di un computer Windows NT o Windows 2000.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




