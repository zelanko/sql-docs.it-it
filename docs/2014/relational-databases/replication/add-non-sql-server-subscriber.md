---
title: Aggiungere un Sottoscrittore non SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.addnonsqlsubscriber.f1
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e36d048b11fcc71b27ab0ab2ee815b0284187c4d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068833"
---
# <a name="add-non-sql-server-subscriber"></a>Aggiungi Sottoscrittore non SQL Server
  La replica supporta la creazione di sottoscrizioni push delle pubblicazioni transazionali e snapshot per i Sottoscrittori Oracle e IBM DB2.  
  
## <a name="options"></a>Opzioni  
 **Tipo di Sottoscrittore da aggiungere**  
 Consente di selezionare un Sottoscrittore Oracle o IBM DB2. Per altre informazioni sul supporto per tali Sottoscrittori, vedere [Sottoscrittori non SQL Server](non-sql/non-sql-server-subscribers.md).  
  
 **Nome origine dati**  
 Nome utilizzato per individuare il database in rete. La replica genera una stringa di connessione per il database utilizzando il nome dell'origine dei dati in combinazione con l'account di accesso, la password e le eventuali opzioni di connessione specificate nella pagina **Sicurezza agente di distribuzione** di questa procedura guidata.  
  
> [!NOTE]  
>  Il nome dell'origine dei dati e la stringa di connessione non vengono convalidati da [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finché l'agente di distribuzione non tenta di inizializzare la sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sottoscrizione per un Sottoscrittore non SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
