---
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3ea7c8720d43fdba53821091c0664bfe375a57b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776803"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3724|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile %S_MSG la %S_MSG '%.*ls' perché è in uso per la replica.|  
  
## <a name="explanation"></a>Spiegazione  
 Quando gli oggetti di un database vengono replicati, vengono contrassegnati come replicati nella tabella di sistema **sysarticles** (per le pubblicazioni snapshot e transazionali) o **sysmergearticles** (per le pubblicazioni di tipo merge). Se si tenta di eliminare un oggetto replicato, viene generato questo errore.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che l'oggetto di database non sia replicato prima di tentare di eliminarlo. Ad esempio:  
  
-   Se l'errore si verifica nel database di pubblicazione, eliminare l'articolo dalla pubblicazione prima di eliminare l'oggetto. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Se l'errore si verifica nel database di sottoscrizione, eliminare la sottoscrizione prima di eliminare l'oggetto. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](subscribe-to-publications.md). Nelle sottoscrizioni a pubblicazioni transazionali è possibile eliminare la sottoscrizione a un singolo articolo anziché all'intera pubblicazione. Per altre informazioni, vedere [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql).  
  
 Se questo errore si verifica in un database non replicato, eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) per verificare che gli oggetti nel database non siano contrassegnati come replicati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
