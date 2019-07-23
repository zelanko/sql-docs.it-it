---
title: Connetti al server (Oracle) - Proprietà connessione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 44e7d219fefe3a4ffc10f1727738a549d2a1b630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903090"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Connetti al server (Oracle) - Proprietà connessione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare la scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** per specificare un'opzione di pubblicazione, ovvero **Gateway** o **Completa**. Dopo aver identificato un server di pubblicazione, questa opzione può essere modificata solo eliminando e riconfigurando il server di pubblicazione. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opzioni  
 **Tipo server di pubblicazione**  
 Selezionare **Gateway** o **Completa**. L'opzione **Completa** è progettata per offrire pubblicazioni snapshot e transazionali con il set completo di caratteristiche supportate per la pubblicazione Oracle. L'opzione **Gateway** consente l'ottimizzazione della progettazione specifica per migliorare le prestazioni per i casi in cui la replica funge da gateway tra i sistemi. Non è possibile utilizzare l'opzione **Gateway** se si intende pubblicare la stessa tabella in più pubblicazioni transazionali. Se si seleziona **Gateway**, una tabella può essere presente al massimo in una pubblicazione transazionale e in un numero qualsiasi di pubblicazioni snapshot.  
  
 **Timeout**  
 Consente di specificare per quanto tempo il server di distribuzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve tentare di eseguire la connessione al server di pubblicazione Oracle prima che si verifichi un timeout.  
  
## <a name="see-also"></a>Vedere anche  
 [Glossario dei termini per la pubblicazione Oracle](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Ottimizzazione delle prestazioni per i server di pubblicazione Oracle](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
