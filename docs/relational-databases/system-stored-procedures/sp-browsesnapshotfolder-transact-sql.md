---
description: sp_browsesnapshotfolder (Transact-SQL)
title: sp_browsesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 11605b404e846db81cd364eac2e9223bf563e3a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493426"
---
# <a name="sp_browsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Restituisce il percorso completo per l'ultimo snapshot generato per una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione contenente l'articolo. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'` Nome del Sottoscrittore. *Subscriber* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @subscriber_db = ] 'subscriber_db'` Nome del database di sottoscrizione. *subscriber_db* è di **tipo sysname**e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Percorso completo della directory snapshot.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_browsesnapshotfolder** viene utilizzata nella replica snapshot e nella replica transazionale.  
  
 Se i campi *Sottoscrittore* e *SUBSCRIBER_DB* vengono lasciati null, il stored procedure restituisce la cartella snapshot dello snapshot più recente che è possibile trovare per la pubblicazione. Se vengono specificati i campi *Sottoscrittore* e *subscriber_db* , il stored procedure restituisce la cartella snapshot per la sottoscrizione specificata. Se per la pubblicazione non è stato generato uno snapshot, viene restituito un set di risultati vuoto.  
  
 Se la pubblicazione è configurata per la generazione di file di snapshot sia nella directory di lavoro che nella cartella snapshot del server di pubblicazione, il set dei risultati include due righe. La prima riga contiene la cartella snapshot della pubblicazione e la seconda la directory di lavoro del server di pubblicazione. **sp_browsesnapshotfolder** è utile per determinare la directory in cui vengono generati i file di snapshot.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_browsesnapshotfolder**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
