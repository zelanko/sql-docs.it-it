---
title: Sys.trusted_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: ''
author: VanMSFT
ms.author: vanto
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9682535c82f8a579259993e82560dfe6bc930f93
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061360"
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Contiene una riga per ogni assembly attendibili per il server.

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|Nome colonna |Tipo di dati |Descrizione |
|--- |--- |--- |
|hash |varbinary(8000 |SHA2_512 hash del contenuto di assembly. |
|description |nvarchar(4000) |Descrizione definita dall'utente facoltativo dell'assembly. Microsoft consiglia di usare il nome canonico che codifica il nome semplice, numero di versione, impostazioni cultura, chiave pubblica e architettura dell'assembly da considerare attendibile. Questo valore identifica in modo univoco identifica l'assembly sul lato di runtime (CLR) di linguaggio comune ed è identico al valore di clr_name in Assemblies. |
|create_date |datetime2 |Data che l'assembly è stato aggiunto all'elenco di assembly attendibili. |
|created_by |nvarchar(128) |Nome di account di accesso dell'entità che ha aggiunto l'assembly all'elenco. |
| | | |


## <a name="remarks"></a>Note  

Uso **necessario aggiungere sp_add_trusted_assembly** e **necessario aggiungere sys.trusted_assemblies** Aggiungi o Rimuovi assembly da `sys.trusted_assemblies`.

## <a name="see-also"></a>Vedere anche  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

