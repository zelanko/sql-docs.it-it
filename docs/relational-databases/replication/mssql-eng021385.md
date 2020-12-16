---
description: MSSQL_ENG021385
title: MSSQL_ENG021385 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 84cd64ba75f7a87fa7d4f93173d8b0537ddc7f93
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469082"
---
# <a name="mssql_eng021385"></a>MSSQL_ENG021385
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21385|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Lo snapshot non è in grado di elaborare la pubblicazione '%s', probabilmente perché sono in corso attività di modifica dello schema o di aggiunta di nuovi articoli.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore viene generato se l'agente snapshot viene eseguito quando il database di pubblicazione è sottoposto a modifiche, ad esempio l'aggiunta o l'eliminazione di articoli e l'esecuzione di modifiche dello schema negli oggetti pubblicati.  
  
## <a name="user-action"></a>Azione dell'utente  
 Riavviare l'agente snapshot dopo che sono state apportate tutte le modifiche al database di pubblicazione. Per altre informazioni, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
