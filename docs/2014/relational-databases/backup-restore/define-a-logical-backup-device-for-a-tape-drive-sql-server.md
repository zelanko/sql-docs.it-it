---
title: Definire un dispositivo di backup logico per un'unità nastro (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14a96a44967c41b185d3196c9d6577f67547e77a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877936"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>Definizione di un dispositivo di backup logico per un'unità nastro (SQL Server)
  In questo argomento viene descritto come definire un dispositivo di backup logico per un'unità nastro in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un dispositivo logico è un nome definito dall'utente tramite cui viene fatto riferimento a un dispositivo di backup fisico specifico, ovvero un file su disco o un'unità nastro.  L'inizializzazione del dispositivo fisico viene eseguita successivamente, quando viene scritto un backup nel dispositivo di backup.  
  
> [!NOTE]  
>  Il supporto per i dispositivi di backup su nastro verrà rimosso in una versione futura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per definire un dispositivo di backup logico per un'unità nastro utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le unità nastro devono essere supportate dal sistema operativo Microsoft Windows.  
  
-   Il dispositivo nastro deve essere collegato fisicamente al computer in cui è in esecuzione un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il backup su dispositivi nastro remoti non è supportato.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **diskadmin** .  
  
 Richiede l'autorizzazione di scrittura sul disco.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Per definire un dispositivo di backup logico per un'unità nastro  
  
1.  Dopo aver stabilito la connessione all'istanza appropriata del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Esplora oggetti fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **Oggetti server**, quindi fare clic con il pulsante destro del mouse su **Dispositivi di backup**.  
  
3.  Scegliere **Nuovo dispositivo di backup**e verrà aperta la finestra di dialogo **Dispositivo di backup** .  
  
4.  Immettere un nome di dispositivo.  
  
5.  Per la destinazione, fare clic su **Nastro** e selezionare un'unità nastro non ancora associata a un altro dispositivo di backup. Se non sono disponibili unità nastro con queste caratteristiche, l'opzione **Nastro** non sarà disponibile.  
  
6.  Per definire il nuovo dispositivo, fare clic su **OK**.  
  
 Per eseguire il backup in questo nuovo dispositivo, aggiungerlo al campo **Backup su** nella finestra di dialogo **Backup database** (**Generale**). Per altre informazioni, vedere [Creare un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>Per definire un dispositivo di backup logico per un'unità nastro  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio mostra come usare [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) per definire un dispositivo di backup logico per un'unità nastro. Nell'esempio seguente viene aggiunto il dispositivo di backup su nastro `tapedump1`con nome fisico `\\.\tape0`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
