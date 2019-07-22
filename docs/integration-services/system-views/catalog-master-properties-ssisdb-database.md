---
title: catalog.master_properties (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 537b9a1d1b0fb84ba26c56aeb2f897d268bb2d03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104839"
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Consente di visualizzare le proprietà di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master.

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Nome della proprietà di Scale Out Master.|  
|property_value|**nvarchar(max)**|Valore della proprietà di Scale Out Master.|

## <a name="remarks"></a>Remarks
Questa vista mostra una riga per ogni proprietà di Scale Out Master. Nelle proprietà visualizzate da questa vista sono inclusi gli elementi seguenti:

|Nome proprietà|Descrizione|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Server SQL in cui si trova il database del log.|
|**LAST_ONLINE_TIME**|Ultima esecuzione online di Scale Out Master.|
|**MACHINE_IP**|IP del computer.|
|**MACHINE_NAME**|Nome del computer.|
|**MASTER_ADDRESS**|Endpoint di Scale Out Master.|
|**MASTER_SERVICE_PORT**|Porta nell'endpoint di Scale Out Master.|
|**SSLCERT_THUMBPRINT**|Identificazione personale di Scale Out Master.|

## <a name="permissions"></a>Autorizzazioni
Tutti i membri del ruolo del database pubblico hanno l'autorizzazione di lettura per questa vista. 
