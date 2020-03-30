---
title: catalog.grant_permission (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- grant_permission stored procedure [Integration Services]
- catalog.grant_permission stored procedure [Integration Services]
ms.assetid: e72cfd52-de66-45e9-98b9-b8580ac7b956
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9053a5ab4ac64bea8104ce7d9079bf891ffa887a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296762"
---
# <a name="cataloggrant_permission-ssisdb-database"></a>catalog.grant_permission (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene concessa un'autorizzazione su un oggetto a protezione diretta nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql
catalog.grant_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @object_type = ] *object_type*  
 Tipo di oggetto a protezione diretta. Nei tipi di oggetti a protezione diretta sono inclusi cartelle (`1`), progetti (`2`), ambienti (`3`) e operazioni (`4`). *object_type* è di tipo **smallint** _._  
  
 [ @object_id = ] *object_id*  
 Identificatore (ID) univoco dell'oggetto a protezione diretta. *object_id* è di tipo **bigint**.  
  
 [ @principal_id = ] *principal_id*  
 ID dell'entità a cui concedere l'autorizzazione. *principal_id* è di tipo **int**.  
  
 [ @permission_type = ] *permission_type*  
 Tipo di autorizzazione da concedere. *permission_type* è di tipo **smallint**.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo)  
  
 1 (object_class non è valido)  
  
 2 (object_id non esiste)  
  
 3 (principal non esiste)  
  
 4 (l'autorizzazione non è valida)  
  
 5 (altro errore)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni ASSIGN_PERMISSIONS sull'oggetto  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  

Questa procedura non può essere chiamata tramite account di accesso autenticati con SQL Server. Non può essere chiamato tramite l'account di accesso sa.
  
## <a name="remarks"></a>Osservazioni  
 Questa stored procedure consente all'utente di concedere i tipi di autorizzazione descritti nella tabella seguente:  
  
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
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Per errori e avvisi relativi, vedere la sezione Valori di codice restituiti.  
  
  
