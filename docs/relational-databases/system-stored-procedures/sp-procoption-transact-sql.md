---
title: sp_procoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: stevestein
ms.author: sstein
ms.openlocfilehash: bc004c611c218324ce2d2d8b764b3ab05cb73e5d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67896592"
---
# <a name="sp_procoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di impostare o di annullare l'esecuzione automatica di una stored procedure. Una stored procedure configurata per l'esecuzione automatica viene eseguita a ogni avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @ProcName = ] 'procedure'`Nome della procedura per la quale impostare un'opzione. la *routine* è di **tipo nvarchar (776)** e non prevede alcun valore predefinito.  
  
`[ @OptionName = ] 'option'`Nome dell'opzione da impostare. L'unico valore per l' *opzione* è **Startup**.  
  
`[ @OptionValue = ] 'value'`Indica se impostare l'opzione su (**true** o **on**) o su OFF (**false** o **off**). *value* è di tipo **varchar (12)** e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o numero di errore (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 Le procedure di avvio devono trovarsi nel database **Master** e non possono contenere parametri di input o output. L'esecuzione delle stored procedure inizia quando tutti i database sono stati recuperati e il messaggio relativo al completamento del recupero viene registrato all'avvio.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene impostata una routine per esecuzione automatica.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 Nell'esempio seguente viene arrestata l'esecuzione automatica di una routine.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>Vedi anche  
 [Eseguire una stored procedure](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
