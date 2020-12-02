---
description: catalog.set_execution_property_override_value
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1d68015c56a6b5552ebee72f661c879c26aef4a1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129631"
---
# <a name="catalogset_execution_property_override_value"></a>catalog.set_execution_property_override_value 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Imposta il valore di una proprietà per un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @execution_id = ] *execution_id*  
 Identificatore univoco per l'istanza di esecuzione. *execution_id* è di tipo **bigint**.  
  
 [ @property_path = ] *property_path*  
 Percorso alla proprietà nel pacchetto. *property_path* è di tipo **nvarchar(4000)**.  
  
 [ @property_value = ] *property_value*  
 Valore di override da assegnare alla proprietà. *property_value* è di tipo **nvarchar(max)** .  
  
 [ @sensitive = ] *sensitive*  
 Quando il valore è 1, la proprietà è importante e viene crittografata quando viene archiviata. Quando il valore è 0, la proprietà non è importante e il valore viene archiviato non crittografato. L'argomento *sensitive* è di tipo **bit**.  
  
## <a name="remarks"></a>Commenti  
 Questa routine esegue la stessa funzione della sezione **Override di proprietà** nella scheda **Avanzate** della finestra di dialogo **Esegui pacchetto**. Il percorso della proprietà deriva dalla proprietà **Percorso del pacchetto** dell'attività del pacchetto.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Utente senza autorizzazioni appropriate.  
  
-   Identificatore di esecuzione non valido  
  
-   Percorso di proprietà non valido  
  
-   Il tipo di dati del valore della proprietà non corrisponde al tipo di dati della proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
