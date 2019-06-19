---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c8e25f71f23742de35dcc8c9629181dd20af2f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046405"
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21899|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21899|  
|Testo del messaggio|Impossibile eseguire la query sul server di pubblicazione reindirizzato '%s' per determinare la presenza di voci sysserver per i Sottoscrittori del server di pubblicazione originale '%s'. Errore '%d', messaggio di errore '%s'.|  
  
## <a name="explanation"></a>Spiegazione  
**sp_validate_redirected_publisher** esegue query sulle tabelle di metadati delle sottoscrizioni del database del server di pubblicazione presente sul server remoto per determinare i Sottoscrittori associati. L'errore 21899 viene restituito in caso di errore di questa query. La query della convalida richiede l'accesso al database pubblicato sul server di pubblicazione reindirizzato. Se l'accesso specificato quando è stato chiamato **sp_adddistpublisher** per il server di pubblicazione originale non è autorizzato ad accedere al database pubblicato sul server di pubblicazione reindirizzato, viene restituito l'errore 21899.  
  
## <a name="user-action"></a>Azione dell'utente  
Controllare il messaggio di errore citato per determinare la causa dell'errore ed eseguire azioni correttive appropriate  
  
