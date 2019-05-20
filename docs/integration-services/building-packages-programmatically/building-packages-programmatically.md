---
title: Compilazione di pacchetti a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d76b84ec492203474f0da8839bfdfb0aa6be6a54
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65729352"
---
# <a name="building-packages-programmatically"></a>Compilazione di pacchetti a livello di programmazione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Se è necessario creare pacchetti in modo dinamico oppure gestire ed eseguire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] all'esterno dell'ambiente di sviluppo, è possibile modificare i pacchetti a livello di programmazione. Questo approccio rende disponibili diverse opzioni:  
  
-   Caricare ed eseguire un pacchetto esistente senza modifiche.  
  
-   Caricare un pacchetto esistente, riconfigurarlo (ad esempio per un'origine dati diversa) ed eseguirlo.  
  
-   Creare un nuovo pacchetto, aggiungere e configurare i componenti oggetto per oggetto e proprietà per proprietà, salvarlo ed eseguirlo.  
  
 È possibile utilizzare il modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per scrivere codice che consenta di creare, configurare ed eseguire pacchetti in qualsiasi linguaggio di programmazione gestito. Ad esempio, è possibile creare pacchetti guidati dai metadati che configurano le relative connessioni oppure origini dati, trasformazioni e destinazioni in base all'origine dati selezionata e alle relative tabelle e colonne.  
  
 In questa sezione viene descritto e illustrato come creare e configurare un pacchetto a livello di programmazione riga per riga. Per scegliere l'opzione di programmazione di pacchetti meno complessa disponibile, è possibile semplicemente caricare ed eseguire un pacchetto esistente senza modifiche, come descritto in [Esecuzione e gestione dei pacchetti a livello di programmazione](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md).  
  
 Un'opzione intermedia, non descritta in questo documento, consiste nel caricare un pacchetto esistente come modello, riconfigurarlo (ad esempio per un'origine dati diversa) ed eseguirlo. È anche possibile utilizzare le informazioni di questa sezione per modificare gli oggetti esistenti in un pacchetto.  
  
> [!NOTE]  
>  Quando si utilizza un pacchetto esistente come modello e si modificano le colonne esistenti nel flusso di dati, può essere necessario rimuovere le colonne esistenti e chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> dei componenti interessati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Creazione di un pacchetto a livello di programmazione](../../integration-services/building-packages-programmatically/creating-a-package-programmatically.md)  
 Viene descritto come creare un pacchetto a livello di programmazione.  
  
 [Aggiunta di attività a livello di programmazione](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
 Viene descritto come aggiungere attività al pacchetto.  
  
 [Connessione di attività a livello di programmazione](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
 Viene descritto come controllare l'esecuzione dei contenitori e delle attività in un pacchetto in base ai risultati dell'esecuzione di un'attività o contenitore precedente.  
  
 [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)  
 Viene descritto come aggiungere gestioni connessioni a un pacchetto  
  
 [Utilizzo delle variabili a livello di programmazione](../../integration-services/building-packages-programmatically/working-with-variables-programmatically.md)  
 Viene descritto come aggiungere e utilizzare variabili durante l'esecuzione di un pacchetto.  
  
 [Gestione degli eventi a livello di programmazione](../../integration-services/building-packages-programmatically/handling-events-programmatically.md)  
 Viene descritto come gestire gli eventi di pacchetti e attività.  
  
 [Abilitazione della registrazione a livello di programmazione](../../integration-services/building-packages-programmatically/enabling-logging-programmatically.md)  
 Viene descritto come abilitare la registrazione per un pacchetto o attività e come applicare filtri personalizzati ai log eventi.  
  
 [Aggiunta dell'attività Flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
 Viene descritto come aggiungere e configurare l'attività Flusso di dati e i relativi componenti.  
  
 [Individuazione dei componenti del flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
 Viene descritto come individuare i componenti installati nel computer locale.  
  
 [Aggiunta dei componenti del flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
 Viene descritto come aggiungere un componente a un'attività Flusso di dati.  
  
 [Connessione dei componenti del flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
 Viene descritto come connettere due componenti di un flusso di dati.  
  
 [Selezione delle colonne di input a livello di programmazione](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
 Viene descritto come selezionare colonne di input tra quelle fornite a un componente dai componenti a monte nel flusso di dati.  
  
 [Salvataggio di un pacchetto a livello di programmazione](../../integration-services/building-packages-programmatically/saving-a-package-programmatically.md)  
 Viene descritto come salvare un pacchetto a livello di programmazione.  
  
## <a name="reference"></a>Riferimento  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Vengono elencati i codici di errore predefiniti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con i relativi nomi simbolici e le descrizioni.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Estensione di pacchetti tramite scripting](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Viene descritto come estendere il flusso di controllo utilizzando l'attività Script e come estendere il flusso di dati utilizzando il componente script.  
  
 [Estensione di pacchetti tramite oggetti personalizzati](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Viene descritto come creare e programmare attività personalizzate, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.  
  
 [Esecuzione e gestione dei pacchetti a livello di programmazione](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 Viene descritto come enumerare, eseguire e gestire pacchetti nelle cartelle in cui sono archiviati.  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Esempi CodePlex relativi ai [prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkID=131204) sul sito Web www.codeplex.com/MSFTISProdSamples  
  
-   Intervento nel blog relativo all'esecuzione del [profiling delle prestazioni delle estensioni personalizzate](https://go.microsoft.com/fwlink/?LinkId=238831) sul sito Web blogs.msdn.com.  

## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
