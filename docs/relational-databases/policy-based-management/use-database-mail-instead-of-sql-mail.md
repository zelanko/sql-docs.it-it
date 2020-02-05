---
title: Usare Posta elettronica database anziché SQL Mail | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c029883591c49c1be52d23a025ff522b4095a6f5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68069148"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>Utilizzo di Posta elettronica database anziché di SQL Mail
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare la vista del catalogo sys.configurations per determinare se l'opzione di configurazione SQL Mail XPS per l'intero server è impostata su ON.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 SQL Mail verrà rimosso in una delle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Per inviare messaggi, utilizzare Posta elettronica database.  
  
 SQL Mail viene eseguito in-process nel servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'esecuzione di SQL Mail si interrompe, anche il server diventa inattivo. Posta elettronica database viene eseguito in un processo distinto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è scalabile e non richiede l'installazione di componenti client MAPI estesi nel server di produzione.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
