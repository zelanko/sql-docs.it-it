---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 996b93f04d9e9fc063bbacbb5f4a7588794ad208
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191512"
---
# <a name="mssqleng014121"></a>MSSQL_ENG014121
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14121|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Al server di distribuzione '%s' sono associati database di distribuzione. Impossibile eliminarlo.|  
  
## <a name="explanation"></a>Spiegazione  
 Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurata come server di distribuzione non può essere rimossa dal ruolo di server di distribuzione poiché all'istanza sono associati database di distribuzione. Questo errore si verifica se si tenta di eliminare un database di distribuzione associato a uno o più server di pubblicazione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per trovare i nomi dei server di pubblicazione e dei database di distribuzione associati a questo server di distribuzione, eseguire [sp_helpdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql) da qualsiasi database nel server di distribuzione.  
  
 Eseguire [sp_dropdistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql) per tutti i database di distribuzione associati al server di distribuzione. Dopo la rimozione di tutte le associazioni di database di distribuzione, è possibile disabilitare la distribuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)   
 [Configurare la distribuzione](configure-distribution.md)  
  
  
