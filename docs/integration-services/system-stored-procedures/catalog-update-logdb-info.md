---
title: catalog.update_logdb_info (database SSISDB) | Microsoft Docs
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
ms.openlocfilehash: 4c4797b3452f64f7fee7a8d5653c13812d0af716
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85674134"
---
# <a name="catalogupdate_logdb_info-ssisdb-database"></a>catalog.update_logdb_info (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/applies-to-version/sqlserver2017.md)]

Consente di aggiornare le informazioni di registrazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out.

## <a name="syntax"></a>Sintassi

```sql
catalog.update_logdb_info [ @server_name = ] server_name, [ @connection_string = ] connection_string
```

## <a name="arguments"></a>Argomenti
[ @server_name = ] *server_name*  
 Server SQL usato per la registrazione di Scale Out. *server_name* è di tipo **nvarchar**.  

 [ @connection_string = ] *connection_string*  
 Stringa di connessione usata per la registrazione di Scale Out. *connection_string* è di tipo **nvarchar**.

 ## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  

## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
   
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
 
