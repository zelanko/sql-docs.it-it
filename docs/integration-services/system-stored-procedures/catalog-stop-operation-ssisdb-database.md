---
title: catalog.stop_operation (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7427a85fa3e8b6f65bb899d008a13f48008e4c0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715792"
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Arresta una convalida o un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @operation_id = ] *operation_id*  
 Identificatore univoco della convalida o dell'istanza di esecuzione. *operation_id* è di tipo **bigint**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ e MODIFY sulla convalida o sull'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Utente senza autorizzazioni appropriate.  
  
-   Identificatore di operazione non valido.  
  
-   Operazione già arrestata.  
  
## <a name="remarks"></a>Remarks  
 Solo un utente per volta deve arrestare un'operazione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se più utenti tentano di arrestare l'operazione, tramite la stored procedure verrà restituito l'esito positivo (valore `0`) al primo tentativo, ma verrà generato un errore ai tentativi successivi.  
  
  
