---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1de5347082ba632af7ef2685a46ed6418904183
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034618"
---
# <a name="mssqlserver_21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21893|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SQLErrorNum21893|  
|Testo del messaggio|I sottoscrittori (%s) del server di pubblicazione originale '%s' non sembrano server remoti per il server di pubblicazione reindirizzato '%s.' Eseguire `sp_addlinkedserver` nel server di pubblicazione reindirizzato per aggiungere questi sottoscrittori come server remoti.|  
  
## <a name="explanation"></a>Spiegazione  
 `sp_validate_redirected_publisher`Nel  vengono utilizzate le tabelle di metadati della sottoscrizione del database del server di pubblicazione sul server remoto per identificare i sottoscrittori associati e viene verificato che vi siano voci associate in master.dbo.sysservers per i sottoscrittori. Questo errore viene restituito se uno dei sottoscrittori identificato non è presente.  
  
 Questo errore non è considerato un errore irreversibile. Gli agenti che rilevano questo errore lo registreranno come messaggio di errore informativo ma non termineranno, poiché un errore, per avere voci del sottoscrittore appropriate sul nuovo server di pubblicazione, ha un impatto limitato sulla replica. Senza una voce adatta per un Sottoscrittore in sysservers, è possibile che alcune attività di gestione delle sottoscrizioni non riescano se vengono eseguite tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, è possibile eseguire queste stesse attività correttamente eseguendo in modo esplicito le stored procedure di gestione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire `sp_addlinkedserver` sul server di pubblicazione reindirizzato per tutti i sottoscrittori identificati per aggiungerli come server remoti. Quindi, eseguire `sp_serveroption` per impostare il bit del sottoscrittore per il server.  
  
  
