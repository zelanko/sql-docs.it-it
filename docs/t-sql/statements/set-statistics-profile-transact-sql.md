---
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3d48de1a5feef4a00b087fded311a2b57169047
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68131926"
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Visualizza informazioni sul profilo di un'istruzione. L'opzione STATISTICS PROFILE è supportata in query ad hoc, viste e stored procedure.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Osservazioni  
 Quando l'opzione STATISTICS PROFILE è impostata su ON, ogni query eseguita restituisce il normale set di risultati, seguito da un set di risultati aggiuntivo che visualizza un profilo dell'esecuzione della query.  
  
 Il set di risultati aggiuntivo include le colonne SHOWPLAN_ALL per la query e le seguenti colonne aggiuntive.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**prime righe**|Numero effettivo di righe restituite da ogni operatore|  
|**Executes**|Numero di esecuzioni dell'operatore|  
  
## <a name="permissions"></a>Autorizzazioni  
 Per utilizzare l'opzione SET STATISTICS PROFILE e visualizzare l'output, gli utenti devono disporre delle autorizzazioni seguenti:  
  
-   Autorizzazioni appropriate per l'esecuzione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Autorizzazione SHOWPLAN su tutti i database contenenti oggetti a cui viene fatto riferimento nelle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Per le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che non restituiscono set di risultati STATISTICS PROFILE, sono necessarie solo le autorizzazioni per eseguire le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che restituiscono set di risultati STATISTICS PROFILE, devono essere completati i controlli per l'autorizzazione di esecuzione delle istruzioni e l'autorizzazione SHOWPLAN in [!INCLUDE[tsql](../../includes/tsql-md.md)]. In caso contrario, viene interrotta l'esecuzione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e non vengono generate le informazioni Showplan.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
