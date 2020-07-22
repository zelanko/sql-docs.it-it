---
title: catalog.effective_object_permissions (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.effective_object_permissions views [Integration Services]
- effective_object_permissions view [Integration Services]
ms.assetid: e70c4ce9-79f5-44df-ac75-6c29b6e38776
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af72db9d78859f9065673aa145bc4b763199b298
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912674"
---
# <a name="catalogeffective_object_permissions-ssisdb-database"></a>catalog.effective_object_permissions (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Vengono visualizzate le autorizzazioni valide per l'entità corrente per tutti gli oggetti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Tipo di oggetto a protezione diretta. Nei tipi di oggetti a protezione diretta sono inclusi cartelle (`1`), progetti (`2`), ambienti (`3`) e operazioni (`4`).|  
|object_id|**bigint**|Identificatore (ID) univoco o chiave primaria dell'oggetto.|  
|permission_type|**smallint**|Tipo di autorizzazione.|  
  
## <a name="remarks"></a>Osservazioni  
 In questa vista vengono visualizzati i tipi di autorizzazione elencati nella tabella seguente:  
  
|Valore di permission_type|Nome dell'autorizzazione|Descrizione dell'autorizzazione|Tipi di oggetti applicabili|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Consente all'entità di leggere le informazioni considerate parte dell'oggetto, ad esempio le proprietà. Non consente all'entità di enumerare o leggere il contenuto di altri oggetti inseriti all'interno dell'oggetto.|Cartella, progetto, ambiente, operazione|  
|`2`|MODIFY|Consente all'entità di modificare le informazioni considerate parte dell'oggetto, ad esempio le proprietà. Non consente all'entità di modificare gli altri oggetti contenuti all'interno dell'oggetto.|Cartella, progetto, ambiente, operazione|  
|`3`|EXECUTE|Consente all'entità di eseguire tutti i pacchetti nel progetto.|Project|  
|`4`|MANAGE_PERMISSIONS|Consente all'entità di assegnare autorizzazioni agli oggetti.|Cartella, progetto, ambiente, operazione|  
|`100`|CREATE_OBJECTS|Consente all'entità di creare oggetti nella cartella.|Cartella|  
|`101`|READ_OBJECTS|Consente all'entità di leggere tutti gli oggetti nella cartella.|Cartella|  
|`102`|MODIFY_OBJECTS|Consente all'entità di modificare tutti gli oggetti nella cartella.|Cartella|  
|`103`|EXECUTE_OBJECTS|Consente all'entità di eseguire tutti i pacchetti di tutti i progetti contenuti nella cartella.|Cartella|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Consente all'entità di gestire le autorizzazioni su tutti gli oggetti nella cartella.|Cartella|  
  
 Vengono valutati solo gli oggetti su cui il chiamante dispone di autorizzazioni. Le autorizzazioni vengono calcolate in base agli elementi seguenti:  
  
-   Autorizzazioni esplicite  
  
-   Autorizzazioni ereditate  
  
-   Appartenenza dell'entità nei ruoli  
  
-   Appartenenza dell'entità nei gruppi  
  
## <a name="permissions"></a>Autorizzazioni  
 Gli utenti possono visualizzare le autorizzazioni valide solo per se stessi e per i ruoli di cui sono membri.  
  
  
