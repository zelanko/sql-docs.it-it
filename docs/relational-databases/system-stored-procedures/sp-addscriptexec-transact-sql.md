---
title: sp_addscriptexec (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00c5b4b94bc0a4347991944ccaa7898e75f244f0
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130691"
---
# <a name="spaddscriptexec-transact-sql"></a>sp_addscriptexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Invia uno script SQL (file con estensione sql) a tutti i Sottoscrittori di una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=** ] **'**_pubblicazione_**'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@scriptfile=** ] **'**_scriptfile_**'**  
 Percorso completo del file script SQL. *scriptfile* viene **nvarchar (4000)**, non prevede alcun valore predefinito.  
  
 [  **@skiperror=** ] **'**_skiperror_**'**  
 Indica se l'agente di distribuzione o di merge deve essere arrestato in caso di errore durante l'elaborazione dello script. *SkipError* viene **bit**, con un valore predefinito è 0.  
  
 **0** = l'agente verrà arrestato.  
  
 **1** = l'agente continua lo script e ignora l'errore.  
  
 [  **@publisher=** ] **'**_editore_**'**  
 Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere usata durante la pubblicazione da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_addscriptexec** viene utilizzata nella replica transazionale, replica e di tipo merge.  
  
 **sp_addscriptexec** non viene usato per la replica snapshot.  
  
 Per utilizzare **sp_addscriptexec**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account del servizio deve disporre di lettura e le autorizzazioni di scrittura per le autorizzazioni di posizione e lettura di snapshot per la posizione in cui gli script vengono archiviate.  
  
 Il [utilità sqlcmd](../../tools/sqlcmd-utility.md) viene usato per eseguire lo script nel sottoscrittore e lo script viene eseguito nel contesto di sicurezza utilizzato dall'agente di distribuzione o dell'agente di Merge durante la connessione al database di sottoscrizione. Quando l'agente viene eseguito su una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il [utilità osql](../../tools/osql-utility.md) viene usato al posto di [sqlcmd](../../tools/sqlcmd-utility.md).  
  
 **sp_addscriptexec** è utile per applicare script a sottoscrittori e Usa [sqlcmd](../../tools/sqlcmd-utility.md) per applicare il contenuto dello script al sottoscrittore. Tuttavia, poiché le configurazioni dei Sottoscrittori sono soggette a variazioni, gli script testati prima dell'invio al server di pubblicazione potrebbero comunque causare errori in un Sottoscrittore. *SkipError* offre la possibilità di avere l'agente di distribuzione o dell'agente di Merge ignorare gli errori e continuare. Uso [sqlcmd](../../tools/sqlcmd-utility.md) per testare gli script prima dell'esecuzione **sp_addscriptexec**.  
  
> [!NOTE]  
>  Gli errori ignorati vengono comunque registrati nella cronologia dell'agente a titolo di riferimento.  
  
 Usando **sp_addscriptexec** per registrare un file di script per le pubblicazioni utilizzando FTP per il recapito di snapshot è supportato solo per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addscriptexec**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire script durante la sincronizzazione &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [Sincronizzare i dati](../../relational-databases/replication/synchronize-data.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
