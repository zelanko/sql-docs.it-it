---
title: Attività Profiling dati e visualizzatore | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6301066549a8008512bef934f9d887349a6b765b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727767"
---
# <a name="data-profiling-task-and-viewer"></a>Attività Profiling dati e visualizzatore

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Profiling dati offre funzionalità di profiling dei dati all'interno del processo di estrazione, trasformazione e caricamento dei dati. L'attività Profiling dati offre i vantaggi seguenti:  
  
-   Analisi più efficace dei dati di origine  
  
-   Migliore comprensione dei dati di origine  
  
-   Assenza di problemi di qualità dei dati prima che vengano inseriti nel data warehouse  
  
> [!IMPORTANT]  
>  L'attività Profiling dati funziona solo con i dati archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'attività non può essere utilizzata con origini dati di terze parti o basate su file.  
  
## <a name="data-profiling-overview"></a>Panoramica del profiling dei dati  
 La qualità dei dati è importante per ogni azienda. La compilazione da parte delle organizzazione di sistemi analitici e di Business Intelligence da integrare nei sistemi transazionali in uso fa sì che l'affidabilità degli indicatori di prestazioni chiave e delle stime basate sul modello di data mining dipenda completamente dalla validità dei dati su cui tali elementi si basano. Benché l'importanza di dati validi per il processo decisionale delle aziende stia aumentando, aumenta anche la sfida posta dalla necessità di garantire la validità di tali dati. I dati affluiscono costantemente a un'organizzazione da origini e sistemi diversi e da un numero elevato di utenti.  
  
 Le metriche della qualità dei dati possono essere difficili da definire in quanto specifici per il dominio o l'applicazione. Un approccio comune alla definizione della qualità dei dati consiste nel profiling dei dati.  
  
 Un profilo dati è una raccolta di statistiche aggregate sui dati che possono includere gli elementi seguenti:  
  
-   Numero di righe della tabella Customer.  
  
-   Numero di valori distinct nella colonna State.  
  
-   Numero di valori Null o mancanti nella colonna Zip.  
  
-   Distribuzione di valori nella colonna City.  
  
-   Livello di attendibilità della dipendenza funzionale della colonna State nella colonna Zip, ovvero lo stato deve essere sempre lo stesso per un determinato valore Zip.  
  
 Le statistiche fornite dal profilo dati consentono di ottenere le informazioni necessarie per ridurre al minimo in modo efficace i possibili problemi di qualità correlati all'utilizzo di dati di origine.  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services e profiling dati  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]il processo di profiling dei dati è costituito dai passaggi seguenti:  
  
 **Passaggio 1: Configurazione dell'attività Profiling dati**  
 L'attività Profiling dati è un'attività che consente di configurare i profili che si desidera calcolare. Viene quindi eseguito il pacchetto contenente l'attività Profiling dati per calcolare i profili. L'attività salva l'output del profilo in formato XML in un file o una variabile del pacchetto.  
  
 **Per ulteriori informazioni:** [Impostazione dell'attività Profiling dati](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **Passaggio 2: Controllo dei profili calcolati dall'attività Profiling dati**  
 Per visualizzare i profili dati calcolati dall'attività Profiling dati, è necessario inviare l'output a un file e quindi utilizzare il visualizzatore del profilo dati. Questo visualizzatore è un'utilità autonoma che consente di visualizzare l'output del profilo in forma di riepilogo e in formato dettagliato con funzionalità di drill-down facoltative.  
  
 **Per ulteriori informazioni:** [Visualizzatore profilo dati](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>Aggiunta di logica condizionale al flusso di lavoro del profiling dei dati  
 L'attività Profiling dati non dispone di caratteristiche incorporate che consentono di utilizzare la logica condizionale per connettere questa attività alle attività a valle basate sull'output del profilo. È possibile, tuttavia, aggiungere tale logica in modo semplice, con operazioni di programmazione ridotte, in un'attività Script. L'attività Script, ad esempio, può eseguire una query XPath sul file di output dell'attività Profiling dati. La query può determinare se la percentuale di valori Null in una colonna specifica supera una determinata soglia. Se la percentuale supera la soglia, è possibile interrompere il pacchetto e risolvere il problema nei dati di origine prima di continuare. Per altre informazioni, vedere [Incorporamento di un'attività Profiling dati nel flusso di lavoro del pacchetto](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 [Pagina relativa allo schema del profiler dati](https://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
