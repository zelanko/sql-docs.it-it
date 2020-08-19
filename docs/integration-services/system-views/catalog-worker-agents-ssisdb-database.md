---
description: catalog.worker_agents (database SSISDB)
title: catalog.worker_agents (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9048a56959de62791b0f952aff086ae513098be2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421945"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Visualizza le informazioni su [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker.

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|ID agente di lavoro dello Scale Out Worker.|
|IsEnabled|**bit**|Indica se Scale Out Worker è abilitato.|
|DisplayName|**nvarchar(256)**|Nome visualizzato di Scale Out Worker.|
|Descrizione|**nvarchar(256)**|Descrizione di Scale Out Worker.|
|MachineName|**nvarchar(256)**|Nome computer di Scale Out Worker.|
|Tag|**nvarchar(max)**|Tag di Scale Out Worker.|
|UserAccount|**nvarchar(256)**|Account che esegue il servizio Scale Out Worker.|
|LastOnlineTime|**datetimeoffset(7)**|Ultima esecuzione online del servizio Scale Out Worker.|

## <a name="remarks"></a>Osservazioni
Questa vista mostra una riga per ogni Scale Out Worker che si connette allo Scale Out Master che interagisce con il catalogo SSISDB.

## <a name="permissions"></a>Autorizzazioni
Per questa vista è necessaria una delle autorizzazioni seguenti:

- Appartenenza al ruolo del database **ssis_admin**

- Appartenenza al ruolo del database **ssis_cluster_executor**

- Appartenenza al ruolo del server **sysadmin**
