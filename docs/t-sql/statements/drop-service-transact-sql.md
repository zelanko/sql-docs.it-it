---
title: DROP SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_SERVICE_TSQL
- DROP SERVICE
dev_langs:
- TSQL
helpviewer_keywords:
- deleting services
- services [Service Broker], removing
- dropping services
- DROP SERVICE statement
- removing services
ms.assetid: 2351bba7-0f2a-4cda-b3b2-6a88b8747c53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b97fc2b789387babcb05d7b0dfe2e39049a317a8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899721"
---
# <a name="drop-service-transact-sql"></a>DROP SERVICE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Elimina un servizio esistente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
  
DROP SERVICE service_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *service_name*  
 Nome del servizio da eliminare. Non è possibile specificare i nomi del server, del database e dello schema.  
  
## <a name="remarks"></a>Osservazioni  
 Non è possibile eliminare un servizio se vi è una priorità di conversazione che fa riferimento a tale servizio.  
  
 Eliminando un servizio vengono eliminati tutti i messaggi per il servizio dalla coda utilizzata dal servizio stesso. Tramite [!INCLUDE[ssSB](../../includes/sssb-md.md)] viene inviato un errore al lato remoto di qualsiasi conversazione aperta che utilizza tale servizio.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'autorizzazione per eliminare un servizio viene assegnata per impostazione predefinita al proprietario del servizio, ai membri del ruolo predefinito del database db_ddladmin or db_owner e ai membri del ruolo predefinito del server sysadmin.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il servizio `//Adventure-Works.com/Expenses`.  
  
```  
DROP SERVICE [//Adventure-Works.com/Expenses] ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
