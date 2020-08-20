---
description: sp_helpdevice (Transact-SQL)
title: sp_helpdevice (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0da4ef24647edd8de4bda1c412afb1410f9d3c14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474122"
---
# <a name="sp_helpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Visualizza informazioni sui dispositivi di backup di Microsoft® SQL Server™.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]È consigliabile utilizzare invece la vista del catalogo [sys. backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @devname = ] 'name'` Nome del dispositivo di backup per cui vengono segnalate le informazioni. Il valore di *Name* è sempre di **tipo sysname**.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|Nome logico del dispositivo.|  
|**physical_name**|**nvarchar(260)**|Nome fisico del file.|  
|**description**|**nvarchar(255)**|Descrizione del dispositivo.|  
|**Stato**|**int**|Numero che corrisponde alla descrizione dello stato nella colonna **Descrizione** .|  
|**cntrltype**|**smallint**|Tipo di controller del dispositivo:<br /><br /> 2 = dispositivo disco<br /><br /> 5 = dispositivo nastro|  
|**size**|**int**|Dimensioni del dispositivo espresse in pagine da 2 KB.|  
  
## <a name="remarks"></a>Osservazioni  
 Se si specifica *Name* , **sp_helpdevice** Visualizza informazioni sul dispositivo di dump specificato. Se il *nome* non è specificato, **sp_helpdevice** Visualizza le informazioni su tutti i dispositivi di dump nella vista del catalogo **sys. backup_devices** .  
  
 I dispositivi di dump vengono aggiunti al sistema utilizzando **sp_addumpdevice**.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono visualizzate le informazioni su tutti i dispositivi di dump in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Stored procedure di motore di database &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
