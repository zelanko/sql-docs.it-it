---
title: sp_dropdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9943e6f3d43ff1b543a86425b2644ee4c46a105c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081508"
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Disinstalla il server di distribuzione. La stored procedure viene eseguita nel server di distribuzione su qualsiasi database, a eccezione del database di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @no_checks = ] no_checks` Indica se cercare gli oggetti dipendenti prima di eliminare il server di distribuzione. *no_checks* viene **bit**, con un valore predefinito è 0.  
  
 Se **0**, **sp_dropdistributor** controlli per assicurarsi che tutti gli oggetti di pubblicazione e la distribuzione oltre il server di distribuzione sono stati eliminati.  
  
 Se **1**, **sp_dropdistributor** Elimina tutti gli oggetti di pubblicazione e la distribuzione prima di disinstallare il server di distribuzione.  
  
`[ @ignore_distributor = ] ignore_distributor` Indica se questa stored procedure viene eseguita senza stabilire la connessione al server di distribuzione. *ignore_distributor* viene **bit**, il valore predefinito è **0**.  
  
 Se **0**, **sp_dropdistributor** si connette al server di distribuzione e rimuove tutti gli oggetti di replica. Se **sp_dropdistributor** non riesce a connettersi al server di distribuzione, la stored procedure ha esito negativo.  
  
 Se **1**, non viene stabilita alcuna connessione al server di distribuzione e gli oggetti di replica non vengono rimossi. Questo valore viene utilizzato se è in corso la disinstallazione del server di distribuzione oppure se il server è offline in modo permanente. Gli oggetti per questo server di pubblicazione nel server di distribuzione vengono rimossi solo dopo la reinstallazione successiva del server di distribuzione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropdistributor** viene utilizzata in tutti i tipi di replica.  
  
 Se sono presenti altri oggetti server di pubblicazione o distribuzione nel server **sp_dropdistributor** ha esito negativo a meno che non **@no_checks** è impostata **1**.  
  
 Questa stored procedure deve essere eseguita dopo l'eliminazione del database di distribuzione eseguendo **sp_dropdistributiondb**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_dropdistributor**.  
  
## <a name="see-also"></a>Vedere anche  
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
