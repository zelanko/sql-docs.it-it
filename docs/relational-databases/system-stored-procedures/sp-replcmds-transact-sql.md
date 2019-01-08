---
title: sp_replcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c868fe69df1f3fd34fe0c1f550507e7db7b6c944
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823425"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce i comandi per le transazioni contrassegnate per la replica. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Il **sp_replcmds** procedure deve essere eseguita solo per risolvere i problemi con la replica.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@maxtrans=**] *maxtrans*  
 Numero di transazioni su cui si desidera ottenere informazioni. *maxtrans* viene **int**, il valore predefinito è **1**, che specifica la transazione successiva in attesa per la distribuzione.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id articolo**|**int**|ID dell'articolo.|  
|**che**|**bit**|Indica se si tratta di un comando parziale.|  
|**comando**|**varbinary(1024)**|Valore del comando.|  
|**xactid**|**binary(10)**|ID della transazione.|  
|**xact_seqno**|**varbinary(16)**|Numero di sequenza della transazione.|  
|**publication_id**|**int**|ID della pubblicazione.|  
|**command_id**|**int**|ID del comando nel [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
|**command_type**|**int**|Tipo di comando.|  
|**originator_srvname**|**sysname**|Server in cui ha origine la transazione.|  
|**originator_db**|**sysname**|Database in cui ha origine la transazione.|  
|**pkHash**|**int**|Solo per uso interno.|  
|**originator_publication_id**|**int**|ID della pubblicazione in cui ha origine la transazione.|  
|**originator_db_version**|**int**|Versione del database in cui ha origine la transazione.|  
|**originator_lsn**|**varbinary(16)**|Identifica il numero di sequenza del file di log (LSN) per il comando nella pubblicazione di origine.|  
  
## <a name="remarks"></a>Note  
 **sp_replcmds** viene usato dal processo di lettura log nella replica transazionale.  
  
 La replica considera il primo client che esegue **sp_replcmds** all'interno di un database come agente di lettura log.  
  
 Questa procedura può generare comandi per tabelle qualificate con il nome del proprietario oppure non qualifica il nome della tabella (impostazione predefinita). L'aggiunta di nomi di tabella qualificati consente di replicare i dati di tabelle di proprietà di un utente specifico di un database in tabelle di proprietà dello stesso utente in un altro database.  
  
> [!NOTE]  
>  Poiché il nome di tabella nel database di origine è qualificato dal nome del proprietario, per la tabella del database di destinazione è necessario specificare lo stesso nome di proprietario.  
  
 I client che tentano di eseguire **sp_replcmds** nello stesso database ricevono l'errore 18752 fino a quando il primo client si disconnette. Dopo il primo client si disconnette, è possibile eseguire un altro client **sp_replcmds**, e diventa il nuovo agente di lettura log.  
  
 Viene aggiunto un numero di messaggi di avviso 18759 sia la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log degli errori e il [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro applicazioni di Windows se **sp_replcmds** è in grado di replicare un comando di testo, perché non è il puntatore di testo recuperate nella stessa transazione.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_replcmds**.  
  
## <a name="see-also"></a>Vedere anche  
 [Messaggi di errore](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
