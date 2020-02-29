---
title: Compilazione di pacchetti a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4227560fbaf3e618a25e3dd214a214ac68a736e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176556"
---
# <a name="building-packages-programmatically"></a>Compilazione di pacchetti a livello di programmazione
  Se è necessario creare pacchetti in modo dinamico oppure gestire ed eseguire pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] all'esterno dell'ambiente di sviluppo, è possibile modificare i pacchetti a livello di programmazione. Questo approccio rende disponibili diverse opzioni:

-   Caricare ed eseguire un pacchetto esistente senza modifiche.

-   Caricare un pacchetto esistente, riconfigurarlo (ad esempio per un'origine dati diversa) ed eseguirlo.

-   Creare un nuovo pacchetto, aggiungere e configurare i componenti oggetto per oggetto e proprietà per proprietà, salvarlo ed eseguirlo.

 È possibile utilizzare il modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per scrivere codice che consenta di creare, configurare ed eseguire pacchetti in qualsiasi linguaggio di programmazione gestito. Ad esempio, è possibile creare pacchetti guidati dai metadati che configurano le relative connessioni oppure origini dati, trasformazioni e destinazioni in base all'origine dati selezionata e alle relative tabelle e colonne.

 In questa sezione viene descritto e illustrato come creare e configurare un pacchetto a livello di programmazione riga per riga. Per scegliere l'opzione di programmazione di pacchetti meno complessa disponibile, è possibile semplicemente caricare ed eseguire un pacchetto esistente senza modifiche, come descritto in [Esecuzione e gestione dei pacchetti a livello di programmazione](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md).

 Un'opzione intermedia, non descritta in questo documento, consiste nel caricare un pacchetto esistente come modello, riconfigurarlo (ad esempio per un'origine dati diversa) ed eseguirlo. È anche possibile utilizzare le informazioni di questa sezione per modificare gli oggetti esistenti in un pacchetto.

> [!NOTE]
>  Quando si utilizza un pacchetto esistente come modello e si modificano le colonne esistenti nel flusso di dati, può essere necessario rimuovere le colonne esistenti e chiamare il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> dei componenti interessati.

## <a name="in-this-section"></a>Contenuto della sezione
 [Creazione di un pacchetto a livello di programmazione](../building-packages-programmatically/creating-a-package-programmatically.md) Viene descritto come creare un pacchetto a livello di programmazione.

 [Aggiunta di attività a livello di codice](../building-packages-programmatically/adding-tasks-programmatically.md) Viene descritto come aggiungere attività al pacchetto.

 [Connessione di attività a livello di programmazione](../building-packages-programmatically/connecting-tasks-programmatically.md) Viene descritto come controllare l'esecuzione dei contenitori e delle attività in un pacchetto in base al risultato dell'esecuzione di un'attività o di un contenitore precedente.

 [Aggiunta di connessioni a livello di codice](../building-packages-programmatically/adding-connections-programmatically.md) Viene descritto come aggiungere gestioni connessioni a un pacchetto.

 [Utilizzo di variabili a livello di programmazione](../building-packages-programmatically/working-with-variables-programmatically.md) Viene descritto come aggiungere e utilizzare le variabili durante l'esecuzione del pacchetto.

 [Gestione degli eventi a livello di programmazione](../building-packages-programmatically/handling-events-programmatically.md) Viene descritto come gestire gli eventi del pacchetto e dell'attività.

 [Abilitazione della registrazione a livello di codice](../building-packages-programmatically/enabling-logging-programmatically.md) Viene descritto come abilitare la registrazione per un pacchetto o un'attività e come applicare filtri personalizzati per registrare gli eventi.

 [Aggiunta dell'attività flusso di dati a livello di programmazione](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md) Viene descritto come aggiungere e configurare l'attività flusso di dati e i relativi componenti.

 [Individuazione di componenti flusso di dati a livello di codice](../building-packages-programmatically/discovering-data-flow-components-programmatically.md) Viene descritto come rilevare i componenti installati nel computer locale.

 [Aggiunta di componenti flusso di dati a livello di codice](../building-packages-programmatically/adding-data-flow-components-programmatically.md) Viene descritto come aggiungere un componente a un'attività flusso di dati.

 [Connessione di componenti flusso di dati a livello di codice](../building-packages-programmatically/connecting-data-flow-components-programmatically.md) Viene descritto come connettere due componenti flusso di dati.

 [Selezione delle colonne di input a livello di codice](../building-packages-programmatically/selecting-input-columns-programmatically.md) Viene descritto come selezionare le colonne di input da quelle fornite a un componente dai componenti upstream nel flusso di dati.

 [Salvataggio di un pacchetto a livello di programmazione](../building-packages-programmatically/saving-a-package-programmatically.md) Viene descritto come salvare un pacchetto a livello di codice.

## <a name="reference"></a>Informazioni di riferimento
 [Integration Services riferimento a errori e messaggi](../integration-services-error-and-message-reference.md) Elenca i codici di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] errore predefiniti con i relativi nomi simbolici e le descrizioni.

## <a name="related-sections"></a>Sezioni correlate
 [Estensione di pacchetti tramite scripting](../extending-packages-scripting/extending-packages-with-scripting.md) Viene descritto come estendere il flusso di controllo utilizzando l'attività script e come estendere il flusso di dati utilizzando il componente script.

 [Estensione di pacchetti con oggetti personalizzati](../extending-packages-custom-objects/extending-packages-with-custom-objects.md) Viene illustrato come creare attività personalizzate del programma, componenti del flusso di dati e altri oggetti di pacchetto da utilizzare in più pacchetti.

 [Esecuzione e gestione dei pacchetti a livello di programmazione](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md) Viene descritto come enumerare, eseguire e gestire i pacchetti e le cartelle in cui sono archiviati.

## <a name="external-resources"></a>Risorse esterne

-   Esempi CodePlex relativi ai [prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkID=131204) sul sito Web www.codeplex.com/MSFTISProdSamples

-   Intervento nel blog relativo all'esecuzione del [profiling delle prestazioni delle estensioni personalizzate](https://go.microsoft.com/fwlink/?LinkId=238831) sul sito Web blogs.msdn.com.

![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.

## <a name="see-also"></a>Vedere anche
 [SQL Server Integration Services](../sql-server-integration-services.md)


