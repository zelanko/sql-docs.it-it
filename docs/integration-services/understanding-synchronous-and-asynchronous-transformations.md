---
description: Informazioni sulle trasformazioni sincrone e asincrone
title: Informazioni sulle trasformazioni sincrone e asincrone | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 849f01ba00bddd67ca2de2c16b6953cff9b06c36
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495157"
---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>Informazioni sulle trasformazioni sincrone e asincrone

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  La differenza tra una trasformazione sincrona e una asincrona in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] può essere definita più facilmente iniziando con una descrizione della trasformazione sincrona. Se la trasformazione sincrona non soddisfa le esigenze specifiche, è possibile che la progettazione richieda una trasformazione asincrona.  
  
## <a name="synchronous-transformations"></a>Trasformazioni sincrone  
 Tramite una trasformazione sincrona le righe in ingresso vengono elaborate e passate nel flusso di dati una alla volta. L'output è sincrono con l'input, ovvero si verifica contemporaneamente. Pertanto, per elaborare una determinata riga, non sono necessarie informazioni su altre righe nel set di dati. Nell'implementazione effettiva le righe vengono raggruppate in buffer mentre vengono passate da un componente al successivo, ma tali buffer sono trasparenti per l'utente ed è possibile presupporre che ogni riga venga elaborata separatamente.  
  
 Un esempio di una trasformazione sincrona è la trasformazione Conversione dati. Per ogni riga in ingresso, il valore nella colonna specificata viene convertito e la riga viene inviata. Ogni operazione di conversione discreta è indipendente da tutte le altre righe del set di dati.  
  
 Per specificare una trasformazione sincrona durante la creazione di script e la programmazione in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], cercare l'ID dell'input di un componente e assegnarlo alla proprietà **SynchronousInputID** degli output del componente. In questo modo al motore flusso di dati viene indicato di elaborare ogni riga dall'input e di inviarla automaticamente agli output specificati. Se si desidera che ogni riga venga inviata a ogni output, non è necessario scrivere codice aggiuntivo per l'output dei dati. Se si usa la proprietà **ExclusionGroup** per specificare che le righe devono essere inviate solo a un gruppo di output, così come nella trasformazione Suddivisione condizionale, è necessario chiamare il metodo **DirectRow** per selezionare la destinazione appropriata per ogni riga. Se si ha un output degli errori, è necessario chiamare **DirectErrorRow** per inviare le righe con problemi all'output degli errori anziché all'output predefinito.  
  
## <a name="asynchronous-transformations"></a>Trasformazioni asincrone  
 La progettazione potrebbe richiedere una trasformazione asincrona quando non è possibile elaborare ogni riga in modo indipendente da tutte le altre. In altri termini, non è possibile passare ogni riga nel flusso di dati quando viene elaborata, ma è invece necessario eseguire l'output dei dati in modo asincrono, ovvero in un momento diverso, rispetto all'input. Negli scenari seguenti è ad esempio necessaria una trasformazione asincrona:  
  
-   Il componente deve acquisire più buffer di dati prima di eseguire l'elaborazione. Un esempio è la trasformazione Ordinamento, in cui il componente deve elaborare il set completo di righe in una singola operazione.  
  
-   Il componente deve combinare righe da più input. Un esempio è la trasformazione Unione, in cui il componente deve esaminare più righe da ogni input e quindi unirle in base all'ordinamento definito.  
  
-   Non esiste una corrispondenza uno-a-uno tra righe di input e righe di output. Un esempio è la trasformazione Aggregazione, in cui il componente deve aggiungere una riga all'output per mantenere i valori di aggregazione calcolati.  
  
 Per specificare una trasformazione asincrona durante la creazione di script e la programmazione in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], assegnare il valore 0 alla proprietà **SynchronousInputID** degli output del componente. . In questo modo si indica al motore flusso di dati di non inviare automaticamente ogni riga agli output. È quindi necessario scrivere codice per inviare ogni riga in modo esplicito all'output appropriato aggiungendola al nuovo buffer di output creato per l'output di una trasformazione asincrona.  
  
> [!NOTE]  
>  Poiché un componente di origine deve anche aggiungere in modo esplicito ogni riga che legge dall'origine dati ai propri buffer di output, un'origine è simile a una trasformazione con output asincroni.  
  
 È anche possibile creare una trasformazione asincrona che emula una trasformazione sincrona copiando in modo esplicito ogni riga di input nell'output. Tramite questo approccio, è possibile rinominare le colonne o convertire tipi o formati di dati. Con questo approccio si verifica tuttavia una riduzione delle prestazioni. È possibile ottenere gli stessi risultati con prestazioni più elevate utilizzando i componenti integrati di Integration Services, ad esempio Copia colonna o Conversione dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una trasformazione sincrona con il componente script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Creazione di una trasformazione asincrona con il componente script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [Sviluppo di un componente di trasformazione personalizzato con output sincroni](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
