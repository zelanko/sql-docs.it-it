---
title: sp_browsemergesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e03232e394adcb6c6ee8fcf208754cf72ca9e951
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85873883"
---
# <a name="sp_browsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce il percorso completo dell'ultimo snapshot generato per una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar (2000)**|Percorso completo della directory snapshot.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_browsemergesnapshotfolder** viene utilizzata nella replica di tipo merge.  
  
 Se la pubblicazione è configurata in modo da generare file di snapshot sia nella directory di lavoro del server di pubblicazione che nella cartella snapshot del server di pubblicazione, nel set di risultati saranno presenti due righe, delle quali la prima contiene la cartella snapshot della pubblicazione e la seconda contiene la directory di lavoro del server di pubblicazione.  
  
 **sp_browsemergesnapshotfolder** è utile per determinare la directory in cui vengono generati i file di snapshot di tipo merge. Il percorso della cartella e il relativo contenuto possono quindi essere copiati su supporti rimovibili e lo snapshot può essere utilizzato per la sincronizzazione di una sottoscrizione da una posizione snapshot alternativa.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_browsemergesnapshotfolder**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
