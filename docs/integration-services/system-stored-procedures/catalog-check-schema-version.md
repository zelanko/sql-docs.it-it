---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d7ec8899e880220dc2011014501a883fafa4470
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295616"
---
# <a name="catalogcheck_schema_version"></a>catalog.check_schema_version 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Determina se lo schema del catalogo SSISDB e i file binari (assembly ISServerExec e SQLCLR) di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono compatibili.  
  
 ISServerExec.exc registra un messaggio di errore quando lo schema e i file binari sono incompatibili.  
  
 La versione dello schema SSISDB viene incrementata quando lo schema cambia durante l'applicazione di patch e aggiornamenti. È consigliabile eseguire questa stored procedure dopo il ripristino di un backup di SSISDB per assicurarsi che lo schema e i file binari siano compatibili.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @use32bitruntime= ] *use32bitruntime*  
 Quando il parametro è impostato su **1**, viene chiamata la versione a 32 bit di dtexec. *use32bitruntime* è di tipo **int**.  
  
## <a name="result-set"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria l'autorizzazioni seguente:  
  
-   Appartenenza al ruolo del database **ssis_admin**.  
  
  
