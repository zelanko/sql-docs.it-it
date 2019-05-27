---
title: Editor destinazione Excel (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldestadapter.connection.f1
helpviewer_keywords:
- Excel Destination Editor
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c55b9daba7e8e1823e1ced43fc9958d4fe5892ff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059235"
---
# <a name="excel-destination-editor-connection-manager-page"></a>Editor destinazione Excel (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione Excel** per specificare le informazioni sull'origine dei dati e visualizzare un'anteprima dei risultati. La destinazione Excel carica i dati in un foglio di lavoro oppure in un intervallo denominato in una cartella di lavoro di [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  Il `CommandTimeout` proprietà della destinazione Excel non è disponibile nel **Editor destinazione Excel**, ma può essere impostata utilizzando la **Editor avanzato**. Inoltre alcune opzioni di caricamento rapido sono disponibili solamente nell' **Editor avanzato**. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla destinazione Excel in [Excel Custom Properties](data-flow/excel-custom-properties.md).  
  
 Per ulteriori informazioni sulla destinazione Excel, vedere [Excel Destination](data-flow/excel-destination.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione Excel**  
 Consente di selezionare una gestione connessione Excel esistente dall'elenco o di creare una nuova connessione facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione nella finestra di dialogo **Gestione connessione Excel** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Carica i dati in un foglio di lavoro o in un intervallo denominato nell'origine dei dati di Excel.|  
|Variabile nome vista o nome tabella|Consente di specificare il foglio di lavoro o il nome dell'intervallo in una variabile.<br /><br /> **Informazioni correlate**: [Uso di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Consente di caricare i dati nella destinazione Excel mediante una query SQL.|  
  
 **Nome del foglio di Excel**  
 Selezionare la destinazione Excel dall'elenco a discesa. Se l'elenco è vuoto, fare clic su **Nuovo**.  
  
 **Nuova**  
 Fare clic su **Nuova** per avviare la finestra di dialogo **Crea tabella** . Quando si fa clic su **OK**viene creato il file di Excel a cui fa riferimento **Gestione connessione Excel** .  
  
 **Visualizza dati esistenti**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
> [!WARNING]  
>  Se la **gestione connessione Excel** selezionata fa riferimento a un file di Excel che non esiste, viene visualizzato un messaggio di errore quando si fa clic su questo pulsante.  
  
## <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome del foglio di Excel**  
 Consente di selezionare il foglio di lavoro o l'intervallo denominato nell'elenco di quelli disponibili nell'origine dei dati.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il nome del foglio di lavoro o dell'intervallo denominato.  
  
### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Digitare il testo di una query SQL, fare clic su **Compila query**per compilare la query oppure scegliere **Sfoglia**per selezionare il file contenente il testo della query.  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici visuali.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione Excel &#40;pagina Mapping&#41;](../../2014/integration-services/excel-destination-editor-mappings-page.md)   
 [Editor destinazione Excel &#40;pagina Output degli errori&#41;](../../2014/integration-services/excel-destination-editor-error-output-page.md)   
 [Esecuzione di un ciclo su file e tabelle di Excel usando un contenitore Ciclo Foreach](control-flow/foreach-loop-container.md)  
  
  
