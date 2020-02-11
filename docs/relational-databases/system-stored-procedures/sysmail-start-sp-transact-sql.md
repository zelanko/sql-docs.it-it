---
title: sysmail_start_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e15996a9db6e1b782875f2dd3d73d0e3e514c8f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044446"
---
# <a name="sysmail_start_sp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Avvia l'esecuzione di Posta elettronica database mediante l'avvio degli oggetti di [!INCLUDE[ssSB](../../includes/sssb-md.md)] utilizzati dal programma esterno.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>Argomenti  
 nessuno  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 Posta elettronica database non viene abilitato né installato durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per abilitare e installare oggetti di Posta elettronica database, utilizzare la Configurazione guidata posta elettronica database.  
  
 Questo stored procedure si trova nel database **msdb** . Questa stored procedure avvia la coda di Posta elettronica database contenente le richieste dei messaggi in uscita e abilita l'attivazione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] per il programma esterno.  
  
 Se le code vengono avviate, il programma esterno Posta elettronica database elabora i messaggi. Questa procedura consente di riavviare le code dopo che le code sono state interrotte con il **sysmail_stop_sp** stored procedure.  
  
> [!NOTE]  
>  Questa stored procedure avvia solo le code di Posta elettronica database e non attiva il recapito dei messaggi di [!INCLUDE[ssSB](../../includes/sssb-md.md)] nel database.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni di esecuzione per questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'avvio di Posta elettronica database nel database **msdb** . Nell'esempio si presuppone che il programma esterno Posta elettronica database sia stato abilitato.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Opzione di configurazione del server Posta elettronica database XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Stored procedure di Posta elettronica database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
