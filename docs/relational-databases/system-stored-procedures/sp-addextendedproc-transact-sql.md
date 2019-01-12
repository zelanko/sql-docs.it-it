---
title: sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 23c97002d5400d3794bed23fea4fb4eb05efd7f0
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133011"
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra il nome di una nuova stored procedure estesa alla [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Usare invece la funzionalità [Integrazione CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@functname =** ] **'**_procedure_**'**  
 Nome della funzione da chiamare all'interno della libreria di collegamento dinamico (DDL, Dynamic-Link Library). *routine* viene **nvarchar(517)**, non prevede alcun valore predefinito. *routine* può includere facoltativamente il nome del proprietario nel formato *proprietario*.  
  
 [  **@dllname =** ] **'**_dll_**'**  
 Nome della DLL che contiene la funzione. *DLL* viene **nvarchar (255)**, non prevede alcun valore predefinito. È consigliabile specificare il percorso completo della DLL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Dopo la creazione di una stored procedure estesa, deve essere aggiunto al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **sp_addextendedproc**. Per altre informazioni, vedere [aggiunta di una Stored Procedure estesa a SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Questa procedura può essere eseguita solo nel **master** database. Per eseguire una stored procedure estesa da un database diverso da **master**, qualificare il nome della stored procedure estesa con **master**.  
  
 **sp_addextendedproc** aggiunge voci per il [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista del catalogo, la registrazione del nome della nuova stored procedure estesa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Viene inoltre aggiunta una voce nel [Sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) vista del catalogo.  
  
> [!IMPORTANT]  
>  Le DLL esistenti non registrate con un percorso completo non funzionano dopo l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per correggere il problema, utilizzare **sp_dropextendedproc** per annullare la registrazione della DLL e quindi registrarla di nuovo **sp_addextendedproc**, specificando il percorso completo.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_addextendedproc**.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente aggiunge il **xp_hello** stored procedure estesa.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
