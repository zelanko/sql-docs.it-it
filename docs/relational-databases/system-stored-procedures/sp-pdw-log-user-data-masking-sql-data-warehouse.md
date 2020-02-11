---
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 18798dece1c801ad0cc4854b7fccc15529a56d5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056455"
---
# <a name="sp_pdw_log_user_data_masking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Usare **sp_pdw_log_user_data_masking** per abilitare la maschera dati utente nei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività. La maschera dati utente influiscono sulle istruzioni in tutti i database nel dispositivo.  
  
> [!IMPORTANT]  
>  I [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività interessati dal **sp_pdw_log_user_data_masking** sono determinati [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività. **sp_pdw_log_user_data_masking** non influisce sui log delle transazioni del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database o sui log degli errori.  
  
 **Sfondo:** Nei log attività di [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] configurazione predefiniti contengono istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] complete e in alcuni casi possono includere dati utente contenuti in operazioni quali le istruzioni **Insert**, **Update**e **Select** . In caso di problemi nell'appliance, questo consente di analizzare le condizioni che hanno causato il problema senza dover riprodurre il problema. Per evitare che i dati utente vengano scritti nei log [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] attività, i clienti possono scegliere di attivare la maschera dati utente utilizzando questo stored procedure. Le istruzioni verranno comunque scritte nei log [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] attività, ma tutti i valori letterali nelle istruzioni che potrebbero contenere dati utente verranno mascherati. sostituito con alcuni valori costanti predefiniti.  
  
 Quando Transparent Data Encryption è abilitato nell'appliance, la maschera dei dati utente nei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività viene attivata automaticamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parametri  
`[ @masking_mode = ] masking_mode`Determina se la maschera dati utente di log Transparent Data Encryption è abilitata. *masking_mode* è di **tipo int**. i possibili valori sono i seguenti:  
  
-   0 = disabilitato, i dati utente vengono [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] visualizzati nei log attività.  
  
-   1 = abilitato, le istruzioni dati utente vengono visualizzate [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nei log attività, ma i dati utente sono mascherati.  
  
-   2 = le istruzioni che contengono dati utente non vengono scritte [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nei log attività.  
  
 L'esecuzione di **sp_pdw_ log_user_data_masking** senza parametri restituisce lo stato corrente della maschera dati utente del log di Transparent Data Mask nell'appliance come set di risultati scalare.  
  
## <a name="remarks"></a>Osservazioni  
 La maschera dati utente nei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività consente la sostituzione di valori letterali con valori costanti predefiniti nelle istruzioni **SELECT** e DML, perché possono contenere dati utente. L'impostazione di *masking_mode* su 1 non maschera i metadati, ad esempio nomi di colonna o di tabella. Impostando *masking_mode* su 2 vengono rimosse le istruzioni con metadati, ad esempio nomi di colonna o di tabella.  
  
 La maschera dati utente nei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività viene implementata nel modo seguente:  
  
-   I dati Transparent Data Encryption [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e utente nei log attività sono disattivati per impostazione predefinita. Le istruzioni non verranno automaticamente mascherate se la crittografia del database non è abilitata nel dispositivo.  
  
-   L'abilitazione di Transparent Data Encryption nell'appliance attiva automaticamente la [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] maschera dati utente nei log attività.  
  
-   La disabilitazione di Transparent Data Encryption non influisce sulla maschera dati utente nei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] log attività.  
  
-   È possibile abilitare in modo esplicito la maschera dati [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] utente nei log attività usando la procedura **sp_pdw_log_user_data_masking** .  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del database **sysadmin** o all'autorizzazione **Control Server** .  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene abilitata la maschera dati utente del log di Transparent nell'appliance.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
