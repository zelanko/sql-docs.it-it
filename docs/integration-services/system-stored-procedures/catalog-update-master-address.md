---
title: catalog.update_master_address (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a400275aa68d9906ad16ae7d1236b019f4e9f6ad
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912747"
---
# <a name="catalogupdate_master_address-ssisdb-database"></a>catalog.update_master_address (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

Consente di aggiornare l'endpoint di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master.

## <a name="syntax"></a>Sintassi

```sql
catalog.update_master_address [ @MasterAddress = ] masterAddress
```

## <a name="arguments"></a>Argomenti
[ @MasterAddress = ] *masterAddress*  
Endpoint di Scale Out Master. *masterAddress* è di tipo **nvarchar**.  

 ## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  

## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
   
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
 
