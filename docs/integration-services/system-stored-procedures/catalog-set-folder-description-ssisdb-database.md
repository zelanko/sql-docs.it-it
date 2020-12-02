---
description: catalog.set_folder_description (database SSISDB)
title: catalog.set_folder_description (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 802416f6-5177-4db5-bca5-976dec5faf53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 18e7cb22f94e33328ed08968052d03b0261c73df
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129644"
---
# <a name="catalogset_folder_description-ssisdb-database"></a>catalog.set_folder_description (database SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Imposta la descrizione di una cartella nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.set_folder_description [ @folder_name = ] folder_name  
    , [ @folder_description = ] folder_description  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @folder_name = ] *folder_name*  
 Nome della cartella. *folder_name* è di tipo **nvarchar(128)** .  
  
 [ @folder_description = ] *folder_description*  
 Descrizione della cartella. *folder_description* è di tipo **nvarchar(MAX)**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Tramite la stored procedure viene restituito un messaggio per confermare l'impostazione della nuova descrizione della cartella.  
  
  
