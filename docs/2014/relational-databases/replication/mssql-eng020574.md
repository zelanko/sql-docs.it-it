---
title: MSSQL_ENG020574 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bc44785fa96b5bc9af8e871605f8304d13bc481d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753283"
---
# <a name="mssqleng020574"></a>MSSQL_ENG020574
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|20574|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|La sottoscrizione del Sottoscrittore '%s' dell'articolo '%s' della pubblicazione '%s' non ha superato la convalida dei dati.|  
  
## <a name="explanation"></a>Spiegazione  
 I dati nel Sottoscrittore sono stati convalidati in base a quelli nel server di pubblicazione e non corrispondono, pertanto la convalida non è stata eseguita. Per ulteriori informazioni sulla convalida, vedere [Validate Replicated Data](validate-replicated-data.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 È consigliabile eseguire le operazioni seguenti:  
  
-   Stabilire i motivi per i quali la convalida non è stata eseguita.  
  
-   Risolvere il problema sottostante che ha causato l'errore.  
  
-   Ripristinare la convergenza dei dati reinizializzando la sottoscrizione oppure utilizzando un altro metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
