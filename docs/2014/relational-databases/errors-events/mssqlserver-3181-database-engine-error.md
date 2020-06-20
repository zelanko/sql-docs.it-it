---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f18509d9a18ba8be1f4e40c93bff5abfcae3d69c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053986"
---
# <a name="mssqlserver_3181"></a>MSSQLSERVER_3181
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|3181|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LDDB_STORAGE_VERIFY|  
|Testo del messaggio|Durante il tentativo di ripristinare questo backup potrebbero verificarsi problemi relativi allo spazio di archiviazione. Ulteriori informazioni verranno fornite nei successivi messaggi.|  
  
## <a name="explanation"></a>Spiegazione  
 Con l'istruzione RESTORE VERIFYONLY viene controllato lo spazio di archiviazione disponibile sul disco in cui il database deve essere ripristinato.  
  
### <a name="possible-causes"></a>Possibili cause  
 È possibile che lo spazio disponibile su disco sia insufficiente per il ripristino del backup verificato.  
  
## <a name="user-action"></a>Azione dell'utente  
 Ripristinare il backup in una posizione con spazio su disco sufficiente oppure aumentare lo spazio sul disco.  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Ripristinare i file in un nuovo percorso &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  
