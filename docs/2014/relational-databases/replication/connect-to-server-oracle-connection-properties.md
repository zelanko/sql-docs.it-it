---
title: Connetti al server (Oracle) - Proprietà connessione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c76a3058283a098357701a44de48efff917acd7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010949"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Connetti al server (Oracle) - Proprietà connessione
  Utilizzare la scheda **Proprietà connessione** della finestra di dialogo **Connetti al server** per specificare un'opzione di pubblicazione, ovvero **Gateway** o **Completa**. Dopo aver identificato un server di pubblicazione, questa opzione può essere modificata solo eliminando e riconfigurando il server di pubblicazione. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opzioni  
 **Tipo di autore**  
 Selezionare **Gateway** o **Completa**. L'opzione **Completa** è progettata per offrire pubblicazioni snapshot e transazionali con il set completo di caratteristiche supportate per la pubblicazione Oracle. L'opzione **Gateway** consente l'ottimizzazione della progettazione specifica per migliorare le prestazioni per i casi in cui la replica funge da gateway tra i sistemi. Non è possibile utilizzare l'opzione **Gateway** se si intende pubblicare la stessa tabella in più pubblicazioni transazionali. Se si seleziona **Gateway**, una tabella può essere presente al massimo in una pubblicazione transazionale e in un numero qualsiasi di pubblicazioni snapshot.  
  
 **Timeout**  
 Specificare per quanto tempo il server di distribuzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve tentare di stabilire la connessione al server di pubblicazione Oracle prima che si verifichi un timeout.  
  
## <a name="see-also"></a>Vedere anche  
 [Glossario dei termini per la pubblicazione Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Ottimizzazione delle prestazioni per i server di pubblicazione Oracle](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
