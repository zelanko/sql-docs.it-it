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
ms.openlocfilehash: 5a45061cc2618407f375150cda4afe744f491c4e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780471"
---
# <a name="mssqlserver_21899"></a>MSSQLSERVER_21899
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
