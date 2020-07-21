---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 197d485fe851298a8e8d365c9fd1a52bf1251101
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553457"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21871|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21871|  
|Testo del messaggio|Il server di pubblicazione %s del database %s non è stato reindirizzato.|  
  
## <a name="explanation"></a>Spiegazione  
 `sp_validate_replica_hosts_as_publishers` controlla la tabella MSredirected_publishers nel database di distribuzione per individuare una voce per il server di pubblicazione identificato e il database del server di pubblicazione.  `sp_validate_replica_hosts_as_publishers` restituisce l'errore 21871 quando non viene trovata alcuna voce.  
  
## <a name="user-action"></a>Azione dell'utente  
 `sp_validate_replica_hosts_as_publishers` è attinente solo per i server di pubblicazione reindirizzati. Se un database del server di pubblicazione è membro di un gruppo di disponibilità, utilizzare la stored procedure `sp_redirect_publisher` per associare il server di pubblicazione e il database del server di pubblicazione al nome del listener del gruppo di disponibilità.  
  
  
