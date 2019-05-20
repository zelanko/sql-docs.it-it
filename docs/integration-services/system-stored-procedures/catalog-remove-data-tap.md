---
title: catalog.remove_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: b77db3e6-478c-441a-a838-82c4de750275
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dab606451fc99c70b28999f2d2d8be93d1513a20
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65716045"
---
# <a name="catalogremovedatatap"></a>catalog.remove_data_tap 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Rimuove un data tap da un output del componente in esecuzione. L'identificatore univoco per la scelta dei dati è associato a un'istanza dell'esecuzione.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.remove_data_tap [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @data_tap_id = ] *data_tap_id*  
 Identificatore univoco per il data tap creato tramite la stored procedure catalog.add_data_tap. *data_tap_id* è di tipo **bigint**.  
  
## <a name="remarks"></a>Remarks  
 Se un pacchetto contiene più di un'attività Flusso di dati con lo stesso nome, il data tap viene aggiunto alla prima attività Flusso di dati con il nome specificato.  
  
## <a name="return-codes"></a>Codici restituiti  
 0 (esito positivo)  
  
 Quando la stored procedure ha esito negativo viene generato un errore.  
  
## <a name="result-set"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Remarks  
 Per rimuovere scelte dei dati, l'istanza di esecuzione deve essere nello stato di creazione (valore di 1 nella colonna **status** della vista [catalog.operations &#40;Database SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)).  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione MODIFY per l'istanza di esecuzione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte le condizioni che causano la mancata riuscita della stored procedure.  
  
-   L'utente non dispone delle autorizzazioni MODIFY.  
  
## <a name="see-also"></a>Vedere anche  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)   
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
