---
title: Visualizzare o configurare l'opzione di configurazione del server backup compression default | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], backup compression default option
- backup compression [SQL Server], backup compression default Option
ms.assetid: 23029395-3e93-4c29-b7d6-e5a47a3526ff
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed7b46308c7ffc39117accbb68dfd68b9847f721
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808749"
---
# <a name="view-or-configure-the-backup-compression-default-server-configuration-option"></a>Visualizzare o configurare l'opzione di configurazione del server backup compression default
  Questo argomento illustra come visualizzare o configurare l'opzione di configurazione del server **Valore predefinito di compressione backup** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oppure [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **backup compression default** è possibile determinare se nell'istanza del server vengono creati backup compressi per impostazione predefinita. Quando è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'opzione **Valore predefinito di compressione backup** è disattivata.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare o configurare l'opzione backup compression default tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione backup compression default](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   La compressione dei backup non è disponibile in tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Per impostazione predefinita, la compressione aumenta significativamente l'utilizzo della CPU, il che può avere un impatto negativo sulle operazioni simultanee. Potrebbe pertanto essere necessario creare backup compressi con priorità bassa in una sessione in cui l'utilizzo della CPU è limitato da [Resource Governor](../../relational-databases/resource-governor/resource-governor.md). Per ulteriori informazioni, vedere [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Quando si crea un singolo backup, si imposta una configurazione di log shipping o si crea un piano di manutenzione, è possibile eseguire l'override dell'impostazione predefinita a livello del server.  
  
-   La compressione dei backup è supportata sia per i dispositivi di backup su disco sia per quelli su nastro.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-configure-the-backup-compression-default-option"></a>Per visualizzare o configurare l'opzione backup compression default  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Impostazioni database** .  
  
3.  Sotto **Backup e ripristino**, **Comprimi backup** viene visualizzata l'impostazione corrente dell'opzione **backup compression default** . Questa impostazione determina l'impostazione predefinita a livello di server per la compressione di backup, come riportato di seguito:  
  
    -   Se la casella **Comprimi backup** è vuota, per impostazione predefinita i nuovi backup non sono compressi.  
  
    -   Se la casella **Comprimi backup** è selezionata, per impostazione predefinita i nuovi backup vengono compressi.  
  
     Se si è un membro del ruolo predefinito del server **sysadmin** o **serveradmin** , è anche possibile modificare l'impostazione predefinita facendo clic sulla casella **Comprimi backup** .  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-view-the-backup-compression-default-option"></a>Per visualizzare l'opzione backup compression default  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio vengono eseguite query sulla vista del catalogo [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) per determinare il valore per `backup compression default`. Il valore 0 indica che la compressione dei backup è disabilitata, mentre il valore 1 che è abilitata.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
SELECT value   
FROM sys.configurations   
WHERE name = 'backup compression default' ;  
GO  
  
```  
  
#### <a name="to-configure-the-backup-compression-default-option"></a>Per configurare l'opzione backup compression default  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per configurare l'istanza del server per creare backup compressi per impostazione predefinita.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_configure 'backup compression default', 1 ;  
RECONFIGURE WITH OVERRIDE ;  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione backup compression default  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)  
  
  
