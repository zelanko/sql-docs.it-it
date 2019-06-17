---
title: Usare Posta elettronica database anziché SQL Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cfce3fb95ddae03525b7f63f09d109c6dc80b47c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62676970"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>Utilizzo di Posta elettronica database anziché di SQL Mail
  Questa regola consente di controllare la vista del catalogo sys.configurations per determinare se l'opzione di configurazione SQL Mail XPS per l'intero server è impostata su ON.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 SQL Mail verrà rimosso in una delle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Per inviare messaggi, utilizzare Posta elettronica database.  
  
 SQL Mail viene eseguito in-process nel servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'esecuzione di SQL Mail si interrompe, anche il server diventa inattivo. Posta elettronica database viene eseguito in un processo distinto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è scalabile e non richiede l'installazione di componenti client MAPI estesi nel server di produzione.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Posta elettronica database](../database-mail/database-mail.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
