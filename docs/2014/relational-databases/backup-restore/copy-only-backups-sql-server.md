---
title: Backup di sola copia (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cba784ed6e81152e91b8320ac5e441187c07df9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922132"
---
# <a name="copy-only-backups-sql-server"></a>Backup di sola copia (SQL Server)
  Un *backup di sola copia* è un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalla sequenza di backup convenzionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In genere, l'esecuzione di un backup comporta la modifica del database e influisce sulla modalità di ripristino dei backup successivi. In alcuni casi, tuttavia, è utile eseguire un backup per uno scopo speciale senza influire sulle procedure generali di backup e ripristino del database. I backup di sola copia hanno questo scopo.  
  
 I tipi di backup di sola copia sono i seguenti:  
  
-   Backup completi di sola copia (tutti i modelli di recupero)  
  
     Un backup di sola copia non può essere utilizzato come base differenziale o come backup differenziale e non influisce sulla base differenziale.  
  
     Ripristinare un backup completo di sola copia equivale al ripristino di un qualsiasi altro backup completo.  
  
-   Backup del log di sola copia (solo modello di recupero con registrazione completa e modello di recupero con registrazione minima delle operazioni bulk)  
  
     Un backup del log di sola copia mantiene il punto di archiviazione del log esistente e pertanto non influisce sulla sequenza dei backup del log regolari. I backup del log di sola copia in genere non sono necessari. È invece possibile creare un nuovo backup del log di routine (con WITH NORECOVERY) e quindi utilizzare il backup in questione insieme a tutti i backup del log precedenti necessari per la sequenza di ripristino. Tuttavia, un backup del log di sola copia può talvolta essere utile per eseguire un ripristino in linea. Per un esempio, vedere [Esempio: Ripristino online di un file di lettura/scrittura &#40;modello di recupero con registrazione completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md).  
  
     Il log delle transazioni non viene mai troncato dopo un backup di sola copia.  
  
 I backup di sola copia vengono registrati nella colonna **is_copy_only** della tabella [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) .  
  
## <a name="to-create-a-copy-only-backup"></a>Per creare un backup di sola copia  
 È possibile creare un backup di sola copia utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell.  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
1.  Nella pagina **Generale** della finestra di dialogo **Backup database** selezionare l'opzione **Backup di sola copia**.  
  
###  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 La sintassi [!INCLUDE[tsql](../../../includes/tsql-md.md)] essenziale è la seguente:  
  
-   Per un backup completo di sola copia:  
  
     BACKUP DATABASE *database_name* TO \<dispositivo_backup *>* ... WITH COPY_ONLY...  
  
    > [!NOTE]  
    >  L'opzione COPY_ONLY non ha alcun effetto quando specificata con l'opzione DIFFERENTIAL.  
  
-   Per un backup del log di sola copia:  
  
     BACKUP LOG *database_name* TO *\<* dispositivo_backup *>* ... WITH COPY_ONLY...  
  
###  <a name="PowerShellProcedure"></a> Utilizzo di PowerShell  
  
1.  Utilizzare il cmdlet `Backup-SqlDatabase` con il parametro `-CopyOnly`.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per creare un backup completo o del log**  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
 **Per visualizzare backup di sola copia**  
  
-   [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
 **Per impostare e utilizzare il provider PowerShell per SQL Server**  
  
-   [Provider PowerShell per SQL Server](../../powershell/sql-server-powershell-provider.md)  
  

  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Modelli di recupero &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Copiare database tramite backup e ripristino](../databases/copy-databases-with-backup-and-restore.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
