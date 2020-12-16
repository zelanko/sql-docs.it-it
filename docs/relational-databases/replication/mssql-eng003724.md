---
description: MSSQL_ENG003724
title: MSSQL_ENG003724 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 9d6bc0ed6bc09dffcd2d88e7b5299c5d66c28660
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475812"
---
# <a name="mssql_eng003724"></a>MSSQL_ENG003724
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|Attributo|valore|  
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
  
-   Se l'errore si verifica nel database di pubblicazione, eliminare l'articolo dalla pubblicazione prima di eliminare l'oggetto. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Se l'errore si verifica nel database di sottoscrizione, eliminare la sottoscrizione prima di eliminare l'oggetto. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md). Nelle sottoscrizioni a pubblicazioni transazionali è possibile eliminare la sottoscrizione a un singolo articolo anziché all'intera pubblicazione. Per altre informazioni, vedere [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Se questo errore si verifica in un database non replicato, eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) per verificare che gli oggetti nel database non siano contrassegnati come replicati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
