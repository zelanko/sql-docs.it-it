---
title: catalog.create_environment (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 66367092-9f6e-40e6-90bd-81efb078ab70
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3cf3917aec1bfed9a02a684b5a86b48ffe7dc5e7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716826"
---
# <a name="catalogcreateenvironment-ssisdb-database"></a>catalog.create_environment (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene creato un ambiente nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.create_environment [@folder_name =] folder_name  
     , [@environment_name =] environment_name  
  [  , [@environment_description =] environment_description ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [@folder_name =] *folder_name*  
 Nome della cartella in cui sarà contenuto l'ambiente. *folder_name* è di tipo **nvarchar(128)**.  
  
 [@environment_name =] *environment_name*  
 Nome dell'ambiente. *environment_name* è di tipo **nvarchar(128)**.  
  
 [@environment_description=] *environment_description*  
 Descrizione dell'ambiente (facoltativa). *environment_description* è di tipo **nvarchar(1024)**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ e MODIFY sulla cartella  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   ruolo del database  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Impossibile trovare il nome della cartella  
  
-   Ambiente che dispone dello stesso nome già presente nella cartella specificata  
  
## <a name="remarks"></a>Remarks  
 Il nome dell'ambiente deve essere univoco all'interno della cartella.  
  
  
