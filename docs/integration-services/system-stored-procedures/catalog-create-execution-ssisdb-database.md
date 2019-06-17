---
title: catalog.create_execution (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 51be58cd1c486a139486839e39a9ac820d7818b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716824"
---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea un'istanza di esecuzione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Questa stored procedure utilizza il livello di registrazione server predefinito.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>Argomenti  
 [@folder_name =] *folder_name*  
 Nome della cartella contenente il pacchetto che deve essere eseguito. *folder_name* è di tipo **nvarchar(128)** .  
  
 [@project_name =] *project_name*  
 Nome del progetto contenente il pacchetto che deve essere eseguito. *project_name* è di tipo **nvarchar(128)** .  
  
 [@package_name =] *package_name*  
 Nome del pacchetto che deve essere eseguito. *package_name* è di tipo **nvarchar(260)** .  
  
 [@reference_id =] *reference_id*  
 Identificatore univoco per un riferimento all'ambiente. Questo parametro è facoltativo. *reference_id* è di tipo **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Viene indicato se il runtime a 32 bit deve essere utilizzato per eseguire il pacchetto in un sistema operativo a 64 bit. Usare il valore 1 per eseguire il pacchetto con il runtime a 32 bit quando in esecuzione in un sistema operativo a 64 bit. Utilizzare il valore pari a 0 per eseguire il pacchetto con il runtime a 64 bit quando in esecuzione in un sistema operativo a 64 bit. Questo parametro è facoltativo. *use32bitruntime* è di tipo **bit**.  
 
 [@runinscaleout =] *runinscaleout*  
 Indica se l'esecuzione è in Scale Out. Usare il valore 1 per eseguire il pacchetto in Scale Out. Usare il valore 0 per eseguire il pacchetto senza Scale Out. Questo parametro è facoltativo. Se non specificato, il valore di questo è impostato su DEFAULT_EXECUTION_MODE in [SSISDB].[catalog].[catalog_properties]. *runinscaleout* è di tipo **bit**. 
 
[@useanyworker =] *useanyworker*  
Indica se a un qualsiasi ruolo di lavoro Scale Out è consentita l'esecuzione.

-   Usare il valore 1 per eseguire il pacchetto con un ruolo di lavoro Scale Out. Quando si imposta `@useanyworker` su true, qualsiasi ruolo di lavoro il cui numero massimo di attività (specificato nel file di configurazione di del ruolo di lavoro) non è stato ancora raggiunto è disponibile per l'esecuzione del pacchetto. Per informazioni sul file di configurazione del ruolo di lavoro, vedere [Ruolo di lavoro di scalabilità orizzontale di Integration Services (SSIS)](../scale-out/integration-services-ssis-scale-out-worker.md).

-   Usare il valore 0 per indicare che non tutti i ruoli di lavoro Scale Out sono autorizzati a eseguire il pacchetto. Quando si imposta `@useanyworker` su false è necessario specificare i ruoli di lavoro autorizzati a eseguire il pacchetto mediante Scale Out Manager oppure chiamando l'istruzione `[catalog].[add_execution_worker]` della stored procedure. Se si specifica un ruolo di lavoro che esegue già un altro pacchetto, il ruolo di lavoro completa l'esecuzione del pacchetto corrente prima di richiedere un'altra esecuzione.

Questo parametro è facoltativo. Se non specificato, il valore viene impostato su 1. *useanyworker* è di tipo **bit**. 
  
 [@execution_id =] *execution_id*  
 Viene restituito l'identificatore univoco per un'istanza di esecuzione. *execution_id* è di tipo **bigint**.  

  
## <a name="remarks"></a>Remarks  
 Un'esecuzione viene utilizzata per specificare i valori del parametro utilizzati da un pacchetto durante una singola istanza di esecuzione del pacchetto.  
  
 Se viene specificato un riferimento all'ambiente con il parametro *reference_id*, i parametri di progetto e di pacchetto vengono popolati dalla stored procedure con valori letterali o valori di riferimento dalle variabili di ambiente corrispondenti. Se viene specificato il riferimento all'ambiente, durante l'esecuzione del pacchetto vengono utilizzati i valori di parametro predefiniti. Per determinare esattamente quali valori vengono usati per un'istanza di esecuzione specifica, usare il valore del parametro di output *execution_id* di questa stored procedure ed eseguire una query sulla vista [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md).  
  
 In un'esecuzione possono essere specificati solo i pacchetti contrassegnati come pacchetti del punto di ingresso. In caso contrario, l'esecuzione non viene completata.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene effettuata una chiamata a catalog.create_execution per creare un'istanza di esecuzione del pacchetto Child1.dtsx, non in Scale Out. Il pacchetto è incluso in Project1 di Integration Services. Nell'esempio viene chiamato catalog.set_execution_parameter_value per impostare i valori per i parametri Parameter1, Parameter2 e LOGGING_LEVEL. Inoltre viene chiamato catalog.start_execution per avviare un'istanza di esecuzione.  
  
```sql  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ e EXECUTE sul progetto e, se applicabile, autorizzazioni READ sull'ambiente a cui si fa riferimento  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  

 Se @runinscaleout è uguale a 1, per questa stored procedure è necessaria una delle autorizzazioni seguenti:
 
-   Appartenenza al ruolo del database **ssis_admin**

-   Appartenenza al ruolo del database **ssis_cluster_executor**

-   Appartenenza al ruolo del server **sysadmin**
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Il pacchetto non esiste.  
  
-   Utente senza autorizzazioni appropriate.  
  
-   L'ambiente di riferimento, *reference_id*, non è valido.  
  
-   Specificato pacchetto che non è un pacchetto del punto di ingresso.  
  
-   Tipo di dati della variabile di ambiente a cui si fa riferimento diverso dal tipo di dati del parametro di progetto o di pacchetto.  
  
-   Progetto o pacchetto in cui sono contenuti parametri che richiedono valori, ma non è stato assegnato alcun valore.  
  
-   Non è possibile trovare le variabili di ambiente a cui si fa riferimento nell'ambiente specificato dal riferimento all'ambiente, *reference_id*.  
  
## <a name="see-also"></a>Vedere anche  
 [catalog.start_execution &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [catalog.add_execution_worker &#40;database SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
