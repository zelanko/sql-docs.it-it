---
title: Ripristinare un backup del database nel modello di recupero con registrazione minima (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e2fd00fd96fe9b0bf7e1b605d935908970d0c1fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875623"
---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>Ripristinare un backup del database nel modello di recupero con registrazione minima (Transact-SQL)
  In questo argomento viene descritto come ripristinare un backup completo del database.  
  
> [!IMPORTANT]  
>  L'amministratore di sistema che esegue il ripristino del backup completo del database deve essere l'unico utente collegato al database.  
  
## <a name="prerequisites-and-recommendations"></a>Prerequisiti e indicazioni  
  
-   Per ripristinare un database crittografato, è necessario poter accedere alla chiave asimmetrica o al certificato utilizzato per crittografare il database. Non è possibile effettuare l'operazione di ripristino del database senza almeno uno di questi due elementi. Di conseguenza, il certificato utilizzato per crittografare la chiave di crittografia del database deve essere conservato fino a quando il backup è necessario. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
-   Per motivi di sicurezza, è consigliabile non collegare o ripristinare database da origini sconosciute o non attendibili. Tali database possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di usare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) sul database in un server non di produzione ed esaminare anche il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  
## <a name="database-compatibility-level-after-upgrade"></a>Livello di compatibilità del database dopo l'aggiornamento  
 I livelli di compatibilità dei database **tempdb**, **model**, **msdb** e **Resource** vengono impostati sul livello di compatibilità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dopo l'aggiornamento. Il database di sistema **master** mantiene il livello di compatibilità precedente all'aggiornamento a meno che tale livello non fosse minore di 100. Se il livello di compatibilità di **master** era minore di 100 prima dell'aggiornamento, viene impostato su 100 dopo l'aggiornamento.  
  
 Se il livello di compatibilità di un database utente è 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità è 90 prima dell'aggiornamento, nel database aggiornato viene impostato su 100, ovvero sul livello di compatibilità supportato più basso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  I nuovi database utente erediteranno il livello di compatibilità del database **model** .  
  
## <a name="procedures"></a>Procedure  
  
#### <a name="to-restore-a-full-database-backup"></a>Per ripristinare un backup completo del database  
  
1.  Eseguire l'istruzione RESTORE DATABASE per ripristinare il backup completo del database, specificando:  
  
    -   Nome del database da ripristinare.  
  
    -   Il dispositivo di backup da cui viene ripristinato il backup completo del database.  
  
    -   La clausola NORECOVERY, se è disponibile un backup del log delle transazioni o un backup differenziale del database da applicare dopo il ripristino del backup completo del database.  
  
    > [!IMPORTANT]  
    >  Per ripristinare un database crittografato, è necessario poter accedere alla chiave asimmetrica o al certificato utilizzato per crittografare il database. Non è possibile effettuare l'operazione di ripristino del database senza almeno uno di questi due elementi. Di conseguenza, il certificato utilizzato per crittografare la chiave di crittografia del database deve essere conservato fino a quando il backup è necessario. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
2.  Facoltativamente, specificare:  
  
    -   La clausola FILE per identificare il set di backup nel dispositivo di backup da ripristinare.  
  
> [!NOTE]  
>  Se si ripristina un database di una versione precedente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene aggiornato automaticamente. In genere, il database diventa subito disponibile. Se tuttavia un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] include indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server  **upgrade_option** . Se l'opzione di aggiornamento è impostata per l'importazione (**upgrade_option** = 2) o la ricompilazione (**upgrade_option** = 0), gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che quando l'opzione di aggiornamento è impostata sull'importazione, gli indici full-text associati vengono ricompilati se non è disponibile un catalogo full-text. Per modificare l'impostazione della proprietà del server **upgrade_option** , usare [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql).  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 In questo esempio viene eseguito un ripristino da nastro del backup completo del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
### <a name="example"></a>Esempio  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md)   
 [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Informazioni sulla cronologia e sull'intestazione del backup &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [Ricompilare database di sistema](../databases/system-databases.md)  
  
  
