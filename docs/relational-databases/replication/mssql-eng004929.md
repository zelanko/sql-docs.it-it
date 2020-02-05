---
title: MSSQL_ENG004929 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG004929 error
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f7666e5b50c257b9d827eefde5bf0853eb9a70cc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286298"
---
# <a name="mssql_eng004929"></a>MSSQL_ENG004929
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|4929|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile modificare %S_MSG '%.*ls' perché è in corso di pubblicazione per la replica.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore si verifica in genere quando si tenta di eliminare il vincolo di chiave primaria di una tabella pubblicata per la replica transazionale. Nella replica transazionale è necessaria una chiave primaria per ogni tabella pubblicata, pertanto il vincolo non può essere eliminato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per eliminare il vincolo, eliminare innanzitutto l'articolo associato alla tabella. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md). Se questo errore si verifica in un database non replicato, eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) per verificare che gli oggetti nel database non siano contrassegnati come replicati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
