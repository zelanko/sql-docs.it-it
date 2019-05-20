---
title: catalog.get_parameter_values (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 391a47edc45145bac21ce351e36c613f2a76addd
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716101"
---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vengono risolti e recuperati i valori predefiniti del parametro da un progetto e dai pacchetti corrispondenti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @folder_name = ] *folder_name*  
 Nome della cartella in cui è contenuto il progetto. *folder_name* è di tipo **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nome del progetto in cui si trovano i parametri. *project_name* è di tipo **nvarchar(128)**.  
  
 [ @package_name = ] *package_name*  
 Nome del pacchetto. Specificare il nome del pacchetto per recuperare tutti i parametri del progetto e i parametri da un pacchetto specifico. Utilizzare NULL per recuperare tutti i parametri del progetto e i parametri da tutti i pacchetti. *package_name* è di tipo **nvarchar(260)**.  
  
 [ @reference_id = ] *reference_id*  
 Identificatore univoco di un riferimento all'ambiente. Questo parametro è facoltativo. *reference_id* è di tipo **bigint**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 Viene restituita una tabella con il formato seguente:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Tipo di parametro. Il valore è `20` per un parametro del progetto e `30` per un parametro del pacchetto.|  
|parameter_data_type|**nvarchar(128)**|Tipo di dati del parametro.|  
|parameter_name|**sysname**|Nome del parametro.|  
|parameter_value|**sql_variant**|Valore del parametro.|  
|sensitive|**bit**|Quando il valore è `1`, il valore del parametro è importante. In caso contrario, il valore è `0`.|  
|required|**bit**|Quando il valore è `1`, il valore del parametro è necessario per avviare l'esecuzione. In caso contrario, il valore è `0`.|  
|value_set|**bit**|Quando il valore è `1`, il valore del parametro è stato assegnato. In caso contrario, il valore è `0`.|  
  
> [!NOTE]  
>  I valori letterali vengono visualizzati non crittografati. **NULL** viene visualizzato al posto dei valori sensibili.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ sul progetto e, se applicabile, autorizzazione READ sull'ambiente a cui si fa riferimento  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Impossibile trovare il pacchetto nella cartella o progetto specificato.  
  
-   Utente senza autorizzazioni appropriate.  
  
-   Riferimento all'ambiente specificato inesistente.  
  
  
