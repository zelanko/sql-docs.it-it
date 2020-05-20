---
title: sp_markpendingschemachange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 91fb437d0b280f8739f0c6d1b6b90efeb73ab3c0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831024"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stored procedure utilizzata per un migliore supporto delle pubblicazioni di tipo merge, in quanto consente agli amministratori di selezionare le modifiche dello schema in sospeso da ignorare, in modo che non vengano replicate. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!CAUTION]  
>  Con l'esecuzione di questa stored procedure è possibile che modifiche dello schema non vengano replicate. È pertanto consigliabile utilizzarla solo per risolvere problemi non risolti con altri metodi, come la reinizializzazione, oppure quando le soluzioni alternative disponibili sono troppo onerose in termini di prestazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @schemaversion = ] schemaversion`Identifica una modifica dello schema in sospeso. *SchemaVersion* è di **tipo int**e il valore predefinito è **0**. Utilizzare [sp_enumeratependingschemachanges &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) per elencare le modifiche dello schema in sospeso per la pubblicazione.  
  
`[ @status = ] 'status'`Indica se una modifica dello schema in sospeso verrà ignorata. *status* è di **tipo nvarchar (10)** e il valore predefinito è **Active**. Se il valore di *status* viene **ignorato**, la modifica dello schema selezionata non verrà replicata.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_markpendingschemachange** viene utilizzato con la replica di tipo merge.  
  
 **sp_markpendingschemachange** è un stored procedure progettato per supportare la replica di tipo merge e deve essere utilizzato solo quando altre azioni correttive, ad esempio la reinizializzazione, non riescono a correggere la situazione o sono troppo onerose in termini di prestazioni.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Vedere anche  
 [sysmergeschemachange &#40;&#41;Transact-SQL](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
