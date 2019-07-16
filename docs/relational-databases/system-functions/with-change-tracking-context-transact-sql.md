---
title: CON CHANGE_TRACKING_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- WITH_CHANGE_TRACKING_CONTEXT_TSQL
- WITH CHANGE_TRACKING_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- WITH CHANGE_TRACKING_CONTEXT
- change tracking [SQL Server], WITH CHANGE_TRACKING_CONTEXT
ms.assetid: 885e33a1-602a-4b94-8380-a63ac935a683
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 90610b8b93d0d03a41c6dbbae6c2a9a4e9678aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950928"
---
# <a name="with-changetrackingcontext-transact-sql"></a>WITH CHANGE_TRACKING_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Abilita il contesto di una modifica da specificare, ad esempio un ID origine, quando i dati sono modificati. Ad esempio, in caso di utilizzo del rilevamento delle modifiche, un'applicazione potrebbe richiedere di distinguere le modifiche effettuate dall'applicazione stessa dalle modifiche effettuate ai dati esterni all'applicazione.  

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
#### <a name="parameters"></a>Parametri  
 *context*  
 Informazioni contestuali fornite dall'applicazione chiamante e memorizzate con le informazioni sul rilevamento delle modifiche per la modifica. *contesto* viene **varbinary(128)** .  
  
 Il valore può essere una costante o una variabile, ma non può essere NULL.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente illustra come impostare il contesto di rilevamento delle modifiche per una modifica dei dati.  
  
```  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di rilevamento delle modifiche &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Rilevare le modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
