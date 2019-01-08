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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba9320a155ca0af5750ca66cf10564227a3197d3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818813"
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
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
 [**@publication=** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@schemaversion=** ] *schemaversion*  
 Identifica una modifica dello schema in sospeso. *SchemaVersion* viene **int**, con valore predefinito è **0**. Uso [sp_enumeratependingschemachanges &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) per elencare le modifiche dello schema in sospeso per la pubblicazione.  
  
 [  **@status=** ] **'***stato***'**  
 Indica se una modifica dello schema in sospeso verrà ignorata. *lo stato* viene **nvarchar(10)** con valore predefinito è **active**. Se il valore di *lo stato* viene **ignorato**, quindi non verrà replicata la modifica dello schema selezionato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_markpendingschemachange** viene usato con la replica di tipo merge.  
  
 **sp_markpendingschemachange** è una stored procedure progettata per il supporto della replica di tipo merge e deve essere utilizzata solo quando altre azioni correttive, ad esempio la reinizializzazione, non sono stato possibile risolvere la situazione o sono troppo onerosi in condizioni delle prestazioni.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Vedere anche  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
