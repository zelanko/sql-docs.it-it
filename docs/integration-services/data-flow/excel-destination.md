---
description: Destinazione Excel
title: Destinazione Excel | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 85b62ff41c9b413c49ff6312e918f648fba430cd
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194827"
---
# <a name="excel-destination"></a>Destinazione Excel

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La destinazione Excel consente di caricare dati in fogli di lavoro o intervalli di una cartella di lavoro di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
  
## <a name="access-modes"></a>Modalità di accesso  
 Sono disponibili tre diverse modalità di accesso ai dati per il caricamento dei dati:  
  
-   Vista o tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Risultato di un'istruzione SQL. La query può essere con parametri.  
  
## <a name="configure-the-excel-destination"></a>Configurare la destinazione Excel  
 Per connettersi a un'origine dei dati, la destinazione Excel usa una gestione connessione Excel che specifica il file di cartella di lavoro da usare. Per altre informazioni, vedere [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 La destinazione Excel include un input regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](./set-the-properties-of-a-data-flow-component.md)  
  
-   [Proprietà personalizzate di Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Editor destinazione Excel (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione Excel** per specificare le informazioni sull'origine dei dati e visualizzare un'anteprima dei risultati. La destinazione Excel carica i dati in un foglio di lavoro oppure in un intervallo denominato in una cartella di lavoro di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  La proprietà **CommandTimeout** della destinazione Excel non è disponibile nell' **Editor destinazione Excel**, tuttavia può essere impostata utilizzando l' **Editor avanzato**. Inoltre alcune opzioni di caricamento rapido sono disponibili solamente nell' **Editor avanzato**. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa alla destinazione Excel in [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione Excel**  
 Consente di selezionare una gestione connessione Excel esistente dall'elenco o di creare una nuova connessione facendo clic su **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione nella finestra di dialogo **Gestione connessione Excel** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Carica i dati in un foglio di lavoro o in un intervallo denominato nell'origine dei dati di Excel.|  
|Variabile nome vista o nome tabella|Consente di specificare il foglio di lavoro o il nome dell'intervallo in una variabile.<br /><br /> **Informazioni correlate**: [Uso di variabili nei pacchetti](../integration-services-ssis-variables.md)|  
|Comando SQL|Consente di caricare i dati nella destinazione Excel mediante una query SQL.|  
  
 **Nome del foglio di Excel**  
 Selezionare la destinazione Excel dall'elenco a discesa. Se l'elenco è vuoto, fare clic su **Nuovo**.  
  
 **Nuovo**  
 Fare clic su **Nuova** per avviare la finestra di dialogo **Crea tabella** . Quando si fa clic su **OK**viene creato il file di Excel a cui fa riferimento **Gestione connessione Excel** .  
  
 **Visualizza dati esistenti**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
### <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
#### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome del foglio di Excel**  
 Consente di selezionare il foglio di lavoro o l'intervallo denominato nell'elenco di quelli disponibili nell'origine dei dati.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il nome del foglio di lavoro o dell'intervallo denominato.  
  
#### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Digitare il testo di una query SQL, fare clic su **Compila query**per compilare la query oppure scegliere **Sfoglia**per selezionare il file contenente il testo della query.  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici visuali.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
## <a name="excel-destination-editor-mappings-page"></a>Editor destinazione Excel (pagina Mapping)
  Utilizzare la pagina **Mapping** della finestra di dialogo **Editor destinazione Excel** per eseguire il mapping tra colonne di input e colonne di destinazione.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di input disponibili nella tabella e le colonne di destinazione.  
  
 **Colonne di destinazione disponibili**  
 Consente di visualizzare l'elenco delle colonne di destinazione disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di destinazione disponibili nella tabella e le colonne di input.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate nella tabella precedente. È possibile modificare i mapping utilizzando l'elenco **Colonne di input disponibili**.  
  
 **Colonna di destinazione**  
 Consente di visualizzare tutte le colonne di destinazione disponibili, indipendentemente dal fatto che siano mappate o meno.  
  
## <a name="excel-destination-editor-error-output-page"></a>Editor destinazione Excel (pagina Output degli errori)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor destinazione Excel** per specificare le opzioni per la gestione degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input o output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (di origine) selezionate nel nodo **Gestione connessione** della finestra di dialogo **Editor origine Excel**.  
  
 **Error (Errore) (Error (Errore)e)**  
 Consente di specificare l'azione da eseguire in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Argomenti correlati:** [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Troncamento**  
 Consente di specificare l'azione da eseguire in caso di troncamenti, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'errore.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Caricare dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
 [Origine Excel](../../integration-services/data-flow/excel-source.md)   
[Gestione connessione Excel](../connection-manager/excel-connection-manager.md)