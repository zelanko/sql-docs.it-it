---
title: sp_enumdsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 092866e2f8efd69ad0baccc73984dcf8a7db051c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891891"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce un elenco di tutti i nomi di origini dei dati ODBC e OLE DB definiti per un server in esecuzione con un account utente specifico di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Nome origine dati**|**sysname**|Nome dell'origine dei dati.|  
|**Descrizione**|**varchar(255)**|Descrizione dell'origine dei dati.|  
|**Tipo**|**int**|Tipo di origine dei dati:<br /><br /> **1** = DSN ODBC<br /><br /> **3** = origine dati OLE DB|  
|**Nome provider**|**varchar(255)**|Nome del provider OLE DB. Il valore è NULL per DSN ODBC.|  
  
## <a name="remarks"></a>Osservazioni  
 Ogni [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio dispone di un contesto utente. ovvero un set di voci del Registro di sistema che include le definizioni delle origini dei dati ODBC disponibili per l'utente. Il contesto utente dipende dal nome utente utilizzato per l'esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ad esempio, se il server è in esecuzione nel contesto utente dell'account di sistema, i DSN restituiti sono tutti DSN di sistema associati all'account di sistema. Se invece il server viene eseguito con un account utente privato, vengono restituiti solo i DSN definiti per tale account privato di tale utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_enumdsn**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_dsninfo &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
