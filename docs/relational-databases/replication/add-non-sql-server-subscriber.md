---
title: Aggiungere un Sottoscrittore non SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9503a9de44f26a4f005669b2bf6d27e761dab25a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726117"
---
# <a name="add-non-sql-server-subscriber"></a>Aggiungi Sottoscrittore non SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La replica supporta la creazione di sottoscrizioni push delle pubblicazioni transazionali e snapshot per i Sottoscrittori Oracle e IBM DB2.  
  
## <a name="options"></a>Opzioni  
 **Tipo di Sottoscrittore da aggiungere**  
 Consente di selezionare un Sottoscrittore Oracle o IBM DB2. Per altre informazioni sul supporto per tali Sottoscrittori, vedere [Sottoscrittori non SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **Nome origine dati**  
 Nome utilizzato per individuare il database in rete. La replica genera una stringa di connessione per il database utilizzando il nome dell'origine dei dati in combinazione con l'account di accesso, la password e le eventuali opzioni di connessione specificate nella pagina **Sicurezza agente di distribuzione** di questa procedura guidata.  
  
> [!NOTE]
>  Il nome dell'origine dei dati e la stringa di connessione non vengono convalidati da [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finché l'agente di distribuzione non tenta di inizializzare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sottoscrizione per un Sottoscrittore non SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Sottoscrizione delle pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
