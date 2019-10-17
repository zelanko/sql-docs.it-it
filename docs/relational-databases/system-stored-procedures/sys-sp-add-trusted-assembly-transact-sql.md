---
title: sys. sp_add_trusted_assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_trusted_assembly_TSQL
- sp_add_trusted_assembly
- sys.sp_add_trusted_assembly_TSQL
- sys.sp_add_trusted_assembly
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_add_trusted_assembly
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb34a814780a46c12c65948bd0b552effaacda4d
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452886"
---
# <a name="syssp_add_trusted_assembly-transact-sql"></a>sys. sp_add_trusted_assembly (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdbmi-xxxx-xxx-md.md)]

Aggiunge un assembly all'elenco di assembly attendibili per il server.

 ![Icona di collegamento all'argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento all'argomento") [convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


## <a name="syntax"></a>Sintassi
```  
sp_add_trusted_assembly 
    [ @hash = ] 'value'
    [ , [ @description = ] 'description' ]
```  

## <a name="remarks"></a>Remarks  

Questa procedura consente di aggiungere un assembly a [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md).

## <a name="arguments"></a>Argomenti

[@hash =] '*valore*'  
Valore hash SHA2_512 dell'assembly da aggiungere all'elenco di assembly attendibili per il server. Gli assembly attendibili possono essere caricati quando [CLR Strict Security](../../database-engine/configure-windows/clr-strict-security.md) è abilitato, anche se l'assembly non è firmato oppure il database non è contrassegnato come attendibile.

[@description =] '*Description*'  
Descrizione facoltativa definita dall'utente dell'assembly. Microsoft consiglia di utilizzare il nome canonico che codifica il nome semplice, il numero di versione, le impostazioni cultura, la chiave pubblica e l'architettura dell'assembly da considerare attendibile. Questo valore identifica in modo univoco l'assembly sul lato Common Language Runtime (CLR) ed è uguale al valore clr_name in sys. Assemblies. 

## <a name="permissions"></a>Permissions

È richiesta l'appartenenza al ruolo predefinito del server `sysadmin` o all'autorizzazione `CONTROL SERVER`.

## <a name="examples"></a>Esempi  

Nell'esempio seguente viene aggiunto un assembly denominato `pointudt` all'elenco di assembly attendibili per il server. Questi valori sono disponibili da [sys. Assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md).     

```  
EXEC sp_add_trusted_assembly 0x8893AD6D78D14EE43DF482E2EAD44123E3A0B684A8873C3F7BF3B5E8D8F09503F3E62370CE742BBC96FE3394477214B84C7C1B0F7A04DCC788FA99C2C09DFCCC, 
N'pointudt, version=0.0.0.0, culture=neutral, publickeytoken=null, processorarchitecture=msil';
```  

## <a name="see-also"></a>Vedere anche  
  [sys. sp_drop_trusted_assembly](sys-sp-drop-trusted-assembly-transact-sql.md)  
  [sys. trusted_assemblies](../../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md)  
  [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  [CLR Strict Security](../../database-engine/configure-windows/clr-strict-security.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

