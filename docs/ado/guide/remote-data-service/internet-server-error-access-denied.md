---
description: 'Errore del server Internet: Accesso negato'
title: 'Errore del server Internet: accesso negato | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8daeb97bd4bcb8a01556f6ece38e977f1cf0068f
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759742"
---
# <a name="internet-server-error-access-denied"></a>Errore del server Internet: Accesso negato
Se viene visualizzato questo errore, in genere significa che Microsoft Internet Information Services (IIS) ha restituito lo stato seguente:  
  
 HTTP_STATUS_DENIED 401  
  
 Verificare che le directory a cui accede IIS dispongano delle autorizzazioni appropriate. Servizi Desktop remoto è in grado di comunicare con un server Web IIS in esecuzione in una delle tre modalità di autenticazione della password, ovvero la richiesta (autenticazione integrata di Windows in Windows 2000). Inoltre, il server Web deve disporre delle autorizzazioni per il computer dell'origine dati se è un computer Windows NT/Windows 2000.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](./rds-fundamentals.md)