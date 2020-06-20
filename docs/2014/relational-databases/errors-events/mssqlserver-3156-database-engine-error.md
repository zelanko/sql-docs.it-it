---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 25b5a037012a6d6b47b91e763a49cfb67b89f43c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054052"
---
# <a name="mssqlserver_3156"></a>MSSQLSERVER_3156
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|3156|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LDDB_CANT_WRITE|  
|Testo del messaggio|Impossibile ripristinare il file '%ls' in '%ls'. Utilizzare WITH MOVE per identificare un percorso valido per il file.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio generico identifica i nomi file logici o fisici dei file di cui è non stato possibile eseguire il ripristino a causa di un problema relativo al percorso specificato.  
  
### <a name="possible-causes"></a>Possibili cause  
 Tra le cause possibili sono incluse le seguenti:  
  
-   Potrebbe essere necessario l'accesso alla directory di Windows specificata.  
  
-   Il percorso potrebbe essere stato digitato in modo non corretto oppure è possibile che il percorso specificato non esista.  
  
-   Il nome file potrebbe essere utilizzato da un file che non può essere sovrascritto.  
  
## <a name="user-action"></a>Azione dell'utente  
 Esaminare i log degli errori alla ricerca di altri messaggi contenenti ulteriori dettagli.  
  
 Correggere il problema relativo al percorso specificato, ad esempio concedendo l'accesso, oppure utilizzare l'opzione WITH MOVE nell'istruzione RESTORE per rilocare il file.  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Ripristinare i file in un nuovo percorso &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
