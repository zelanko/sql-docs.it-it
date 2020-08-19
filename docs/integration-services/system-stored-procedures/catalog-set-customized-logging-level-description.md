---
description: catalog.set_customized_logging_level_description
title: catalog.set_customized_logging_level_description | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6ceaa39f-2439-457b-b99f-f12d88a1be32
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 99d413f8447a79331f92229a295192b6c0c5ea72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422135"
---
# <a name="catalogset_customized_logging_level_description"></a>catalog.set_customized_logging_level_description 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  Modifica la descrizione di un livello di registrazione personalizzato esistente. Per altre informazioni sui livelli di registrazione personalizzati, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.set_customized_logging_level_description [ @level_name = ] level_name  
    , [ @level_description = ] level_description  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @level_name = ] *level_name*  
 Nome di un livello di registrazione personalizzato esistente.  
  
 *level_name* è di tipo **nvarchar(128)**.  
  
 [ @level_description = ] *level_description*  
 Nuova descrizione del livello di registrazione personalizzato specificato.  
  
 *level_description* è di tipo **nvarchar(1024)**.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="return-codes"></a>Codici restituiti  
 0 (esito positivo)  
  
 Quando la stored procedure ha esito negativo viene generato un errore.  
  
## <a name="result-set"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte le condizioni che causano la mancata riuscita della stored procedure.  
  
-   L'utente non ha le autorizzazioni necessarie.  
  
  
