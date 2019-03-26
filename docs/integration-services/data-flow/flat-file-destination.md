---
title: Destinazione file flat | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96badece6d707558fa9fcda87bdf9f71af64255e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290437"
---
# <a name="flat-file-destination"></a>file flat - destinazione
  La destinazione file flat scrive dati in un file di testo che può essere in formato delimitato, a larghezza fissa, a larghezza fissa con delimitatore di riga o non allineato a destra.  
  
 Per configurare la destinazione file flat, procedere nel modo seguente:  
  
-   Specificare un blocco di testo inserito nel file prima di iniziare a scrivere i dati. Il testo può ad esempio contenere le intestazioni delle colonne.  
  
-   Specificare se sovrascrivere i dati eventualmente presenti in un file di destinazione con lo stesso nome.  
  
 Per accedere al file di testo, questa destinazione utilizza una gestione connessione file flat. Impostando le proprietà della gestione connessione file flat utilizzata dalla destinazione file flat è possibile specificare la modalità con cui la destinazione file flat deve formattare e scrivere il file di testo. Durante la configurazione della gestione connessione file flat si specificano informazioni sul file e sulle singole colonne nel file. È ad esempio possibile specificare i caratteri che delimitano le righe e le colonne del file, oltre al tipo di dati e alla lunghezza di ogni colonna. Per ulteriori informazioni, vedere [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 La destinazione file flat include la proprietà personalizzata Header, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate del file flat](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Questa destinazione include un solo output. Non supporta un output degli errori.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Configurazione della destinazione file flat  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate del file flat](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà di un componente del flusso di dati, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>Editor destinazione file flat (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione file flat** per selezionare la connessione file flat per la destinazione e specificare se eseguire la sovrascrittura o l'accodamento al file di destinazione esistente. La destinazione file flat scrive dati in un file di testo che può essere in formato delimitato, a larghezza fissa o misto, a larghezza fissa con delimitatori di riga oppure non allineato a destra.  
  
### <a name="options"></a>Opzioni  
 **Gestione connessione file flat**  
 Usare la casella di riepilogo per selezionare una gestione connessione esistente oppure fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuova**  
 Consente di creare una nuova connessione utilizzando le finestre di dialogo **Formato file flat** e **Editor gestione connessione file flat** .  
  
 Oltre ai formati file flat standard di larghezza delimitata e fissa e non allineati a destra, la finestra di dialogo **Formato file flat** dispone di una quarta opzione, **Larghezza fissa con delimitatori di riga**. Questa opzione rappresenta un caso speciale del formato non allineato a destra nel quale [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aggiunge una colonna fittizia come colonna finale dei dati. Questa colonna fittizia assicura che la colonna finale abbia una larghezza fissa.  
  
 L'opzione **Larghezza fissa con delimitatori di riga** non è disponibile in **Editor gestione connessione file flat**. Se necessario, è possibile emulare questa opzione nell'editor. Per emulare questa opzione, nella pagina **Generale** dell' **Editor gestione connessione file flat**selezionare **Non allineato a destra**in **Formato**. Quindi, nella pagina **Avanzate** dell'editor aggiungere una nuova colonna fittizia come colonna finale dei dati.  
  
 **Sovrascrivi dati nel file**  
 Consente di indicare se sovrascrivere un file esistente o accodare i dati al file.  
  
 **Intestazione**  
 Consente di digitare un blocco di testo da inserire nel file prima che i dati vengano scritti. Utilizzare questa opzione per includere informazioni aggiuntive, quali le intestazioni delle colonne.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
## <a name="flat-file-destination-editor-mappings-page"></a>Editor destinazione file flat (pagina Mapping)
  Utilizzare la pagina **Mapping** della finestra di dialogo **Editor destinazione file flat** per eseguire il mapping tra le colonne di input e quelle di destinazione.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di input disponibili e le colonne di destinazione.  
  
 **Colonne di destinazione disponibili**  
 Consente di visualizzare l'elenco delle colonne di destinazione disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di destinazione disponibili e le colonne di input.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate più indietro in questo argomento. È possibile modificare i mapping utilizzando l'elenco **Colonne di input disponibili**. Selezionare **\<ignora>** per escludere la colonna dall'output.  
  
 **Colonna di destinazione**  
 Consente di visualizzare tutte le colonne di destinazione disponibili, indipendentemente dal fatto che siano mappate o meno.  
  
## <a name="see-also"></a>Vedere anche  
 [Origine file flat](../../integration-services/data-flow/flat-file-source.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
