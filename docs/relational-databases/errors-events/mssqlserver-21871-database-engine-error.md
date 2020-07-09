---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2dd09da4c151119eb4b7fdf9acceb82fdedf383
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780531"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|21871|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21871|  
|Testo del messaggio|Il server di pubblicazione %s del database %s non è stato reindirizzato.|  
  
## <a name="explanation"></a>Spiegazione  
**sp_validate_replica_hosts_as_publishers** controlla la tabella MSredirected_publishers nel database di distribuzione per cercare una voce per il server di pubblicazione identificato e il database del server di pubblicazione.  **sp_validate_replica_hosts_as_publishers** restituisce l'errore 21871 quando non viene trovata alcuna voce.  
  
## <a name="user-action"></a>Azione dell'utente  
**sp_validate_replica_hosts_as_publishers** è attinente solo per i server di pubblicazione reindirizzati. Se un database del server di pubblicazione è membro di un gruppo di disponibilità, usare la stored procedure **sp_redirect_publisher** per associare il server di pubblicazione e il database del server di pubblicazione al nome del listener del gruppo di disponibilità.  
  
