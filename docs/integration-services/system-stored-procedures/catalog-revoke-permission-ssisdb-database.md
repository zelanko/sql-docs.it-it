---
title: catalog.revoke_permission (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- revoke_permission stored procedure [Integration Services]
- catalog.revoke_permission stored procedure [Integration Services]
ms.assetid: 850b9c26-5c7c-47b9-a61c-5cf9bb5948cf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4853ade7b4888ae8471f05230672e097e87f3131
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132081"
---
# <a name="catalogrevokepermission-ssisdb-database"></a>catalog.revoke_permission (database SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene revocata un'autorizzazione su un oggetto a protezione diretta nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql
catalog.revoke_permission [ @object_type = ] object_type  
    , [ @object_id = ] object_id  
    , [ @principal_id = ] principal_id  
    , [ @permission_type = ] permission_type  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @object_type = ] *object_type*  
 Tipo di oggetto a protezione diretta. Nei tipi di oggetti a protezione diretta sono inclusi cartelle (`1`), progetti (`2`), ambienti (`3`) e operazioni (`4`). *object_type* è di tipo **smallint**_._  
  
 [ @object_id = ] *object_id*  
 Identificatore (ID) univoco dell'oggetto a protezione diretta. *object_id* è di tipo **bigint**.  
  
 [ @principal_id = ] *principal_id*  
 ID dell'entità a cui revocare l'autorizzazione. *principal_id* è di tipo **int**.  
  
 [ @permission_type = ] *permission_type*  
 Tipo di autorizzazione. *permission_type* è di tipo **smallint**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo)  
  
 1 (object_class non è valido)  
  
 2 (object_id non esiste)  
  
 3 (principal non esiste)  
  
 4 (permission non è valido)  
  
 5 (altro errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Remarks  
 None  
  
## <a name="permissions"></a>Permissions  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni ASSIGN_PERMISSIONS sull'oggetto  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="remarks"></a>Remarks  
 Se permission_type viene specificato, la stored procedure rimuove l'autorizzazione assegnata in modo esplicito all'entità per l'oggetto. Anche se non esiste nessuna di tali istanze, tramite la routine viene restituito un valore di codice con esito positivo (`0`). Se permission_type viene omesso, la stored procedure rimuove tutte le autorizzazioni dell'entità sull'oggetto.  
  
> [!NOTE]  
>  L'entità può disporre ancora dell'autorizzazione specificata sull'oggetto se è membro di un ruolo che dispone dell'autorizzazione specificata.  
  
 Questa stored procedure consente all'utente di revocare i tipi di autorizzazione descritti nella tabella seguente:  
  
|Valore di permission_type|Nome dell'autorizzazione|Descrizione dell'autorizzazione|Tipi di oggetti applicabili|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Consente all'entità di leggere le informazioni considerate parte dell'oggetto, ad esempio le proprietà. Non consente all'entità di enumerare o leggere il contenuto di altri oggetti inseriti all'interno dell'oggetto.|Cartella, progetto, ambiente, operazione|  
|`2`|MODIFY|Consente all'entità di modificare le informazioni considerate parte dell'oggetto, ad esempio le proprietà. Non consente all'entità di modificare gli altri oggetti contenuti all'interno dell'oggetto.|Cartella, progetto, ambiente, operazione|  
|`3`|EXECUTE|Consente all'entità di eseguire tutti i pacchetti nel progetto.|Progetto|  
|`4`|MANAGE_PERMISSIONS|Consente all'entità di assegnare autorizzazioni agli oggetti.|Cartella, progetto, ambiente, operazione|  
|`100`|CREATE_OBJECTS|Consente all'entità di creare oggetti nella cartella.|Cartella|  
|`101`|READ_OBJECTS|Consente all'entità di leggere tutti gli oggetti nella cartella.|Cartella|  
|`102`|MODIFY_OBJECTS|Consente all'entità di modificare tutti gli oggetti nella cartella.|Cartella|  
|`103`|EXECUTE_OBJECTS|Consente all'entità di eseguire tutti i pacchetti di tutti i progetti contenuti nella cartella.|Cartella|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Consente all'entità di gestire le autorizzazioni su tutti gli oggetti nella cartella.|Cartella|  
  
  
