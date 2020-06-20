---
title: Le tabelle di cronologia di backup o ripristino di grandi dimensioni rendono l'aggiornamento apparentemente non risponde | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 918c20f58c00c535d8ed41d887e9671f5e821a17
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059222"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>Se sono presenti tabelle di cronologia di backup o ripristino di grandi dimensioni, l'aggiornamento potrebbe sembrare che non risponde
  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono state aggiunte nuove colonne ad alcune delle tabelle di cronologia di backup e ripristino. Per aggiornare queste tabelle, è necessario modificarle in modo da aggiungere le nuove colonne. Se una o più di queste tabelle contengono un numero elevato di righe, l'aggiornamento richiederà molto tempo per l'istruzione ALTER TABLE che aggiunge colonne a tale tabella.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 L'aggiornamento può sembrare non risponde se una delle tabelle di cronologia di backup o ripristino seguenti contiene un numero elevato di righe:  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 Se una di queste tabelle contiene almeno 10.000 righe, verrà segnalato un errore di non conformità. La tabella che supera il numero consentito di righe non viene indicata. La prima tabella che supera le 10.000 righe genera l'errore.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Prima di aggiornare un database, se una di queste tabelle supera le 10.000 righe, si consiglia di ridurre questo numero. Per ridurre le righe in tutte le tabelle, è possibile eseguire il **sp_delete_backuphistory** stored procedure. Questa procedura elimina le voci in tutte le tabelle di cronologia di backup e ripristino relative a set di backup precedenti a una data specificata. Per altre informazioni, vedere [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql).  
  
> [!NOTE]  
>  È possibile aggiornare un database le cui tabelle di cronologia di backup e ripristino contengono più di 10.000 righe, ma il processo potrebbe sembrare bloccato durante la modifica di tabelle di grandi dimensioni. Le dimensioni delle tabelle influiscono sul tempo richiesto per completare il programma di installazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
