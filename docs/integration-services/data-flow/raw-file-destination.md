---
title: Destinazione file non elaborato | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 417fce6637f17b428f0e4d45404760088a8c0e20
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488597"
---
# <a name="raw-file-destination"></a>file non elaborato - destinazione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione file non elaborato scrive dati non elaborati in un file. Poiché il formato dei dati è nativo della destinazione, non è necessaria alcuna conversione e quasi nessuna analisi dei dati. Questo significa che la destinazione file non elaborato è in grado di scrivere i dati più rapidamente rispetto ad altre destinazioni, quali le destinazioni file flat e OLE DB.  
  
 Oltre alla scrittura di dati non elaborati in un file, la destinazione file non elaborato può essere utilizzata anche per generare un file non elaborato vuoto contenente solo le colonne (file di soli metadati), senza dover eseguire il pacchetto. Si utilizza l'origine file non elaborato per recuperare dati non elaborati scritti in precedenza dalla destinazione. È anche possibile puntare l'origine file non elaborato al file di soli metadati.  
  
 Nel formato di file non elaborato sono contenute informazioni di ordinamento. Con la destinazione file non elaborato è possibile salvare tutte le informazioni di ordinamento in cui sono inclusi i flag di confronto per le colonne stringa. Con l'origine file non elaborato è possibile leggere e riconoscere le informazioni di ordinamento. È possibile configurare l'origine file non elaborato in modo da ignorare i flag di ordinamento nel file utilizzando l'editor avanzato. Per altre informazioni sui flag di confronto, vedere [Confronto di dati stringa](../../integration-services/data-flow/comparing-string-data.md).  
  
 Per configurare la destinazione file non elaborato, procedere nel modo seguente:  
  
-   Specificare una modalità di accesso, ovvero il nome del file o una variabile contenente il nome del file in cui la destinazione file non elaborato dovrà scrivere.  
  
-   Indicare se la destinazione file non elaborato deve creare un nuovo file o accodare i dati a un file esistente con lo stesso nome.  
  
 La destinazione file non elaborato viene frequentemente utilizzata per scrivere risultati intermedi di dati parzialmente elaborati durante l'esecuzione dei pacchetti. Se si archiviano i dati non elaborati, sarà possibile rileggerli rapidamente tramite un'origine file non elaborato e quindi trasformarli ulteriormente prima di caricarli nella destinazione finale. È ad esempio possibile eseguire più volte un pacchetto che a ogni esecuzione scrive dati non elaborati in uno o più file e successivamente eseguire un altro pacchetto che utilizza l'origine file non elaborato per leggere i dati da ogni file, utilizza una trasformazione Unione input multipli per unire i dati in un unico set di dati, quindi applica ulteriori trasformazioni che riepilogano i dati prima di caricarli nella destinazione finale, ad esempio una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  La destinazione file non elaborato supporta dati Null ma non dati BLOB (Binary Large Object).  
  
> [!NOTE]  
>  La destinazione file non elaborato non utilizza alcuna gestione connessione.  
  
 Questa origine include un solo input regolare. Non supporta un output degli errori.  
  
## <a name="append-and-new-file-options"></a>Opzioni Accoda e Nuovo file  
 La proprietà WriteOption include opzioni per accodare dati a un file esistente o crearne uno nuovo.  
  
 La tabella seguente descrive le opzioni disponibili per la proprietà WriteOption.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Accoda|Accoda i dati a un file esistente. I metadati dei dati accodati devono corrispondere al formato del file.|  
|Crea sempre|Crea sempre un nuovo file.|  
|Crea una sola volta|Crea un nuovo file. Se il file esiste, il componente ha esito negativo.|  
|Tronca e accoda|Tronca un file esistente e quindi vi scrive i dati. I metadati dei dati accodati devono corrispondere al formato del file.|  
  
 Di seguito sono riportati elementi importanti relativi all'accodamento dei dati:  
  
-   L'accodamento dei dati in un file non elaborato esistente non comporta il riordinamento dei dati.  
  
     È necessario assicurarsi che le chiavi ordinate rimangano nell'ordine corretto.  
  
-   L'accodamento dei dati in un file non elaborato esistente non comporta la modifica dei metadati del file (informazioni sull'ordinamento).  
  
 Ad esempio, in un pacchetto vengono letti i dati ordinati sul ProductKey (PK). Con il flusso di dati del pacchetto, i dati vengono accodati in un file non elaborato esistente. Alla prima esecuzione del pacchetto, vengono ricevute tre righe (PK 1000, 1100, 1200). Nel file non elaborato sono ora contenuti i dati riportati di seguito.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 Alla seconda esecuzione del pacchetto, vengono ricevute due nuove righe (PK 1001, 1300). Nel file non elaborato sono ora contenuti i dati riportati di seguito.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 I nuovi dati vengono accodati alla fine del file non elaborato e le chiavi ordinate (PK) non sono disponibili. Inoltre, l'operazione di accodamento non ha modificato i metadati del file (informazioni di ordinamento). Se il file viene letto utilizzando l'origine file non elaborato, tramite il componente viene indicato che il file è ancora ordinato su PK anche se i dati nel file non sono più nell'ordine corretto.  
  
 Per mantenere le chiavi ordinate nell'ordine corretto mentre si accodano i dati, è possibile progettare il flusso di dati del pacchetto nel modo seguente:  
  
1.  Recuperare le nuove righe tramite l'origine A.  
  
2.  Recuperare le righe esistenti da RawFile1 utilizzando l'origine B.  
  
3.  Combinare gli input delle origini A e B tramite la trasformazione Unione input multipli.  
  
4.  Ordinare su PK.  
  
5.  Scrivere in RawFile2 utilizzando la destinazione file non elaborato.  
  
     RawFile1 viene bloccato perché ne viene eseguita la lettura nel flusso di dati.  
  
6.  Sostituire RawFile1 con RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Utilizzo della destinazione file non elaborato in un ciclo  
 Se il flusso di dati che utilizza la destinazione file non elaborato si trova in un ciclo, può rivelarsi utile creare il file una sola volta e quindi accodare i dati al file quando il ciclo viene ripetuto. Per accodare i dati al file, è necessario che i dati accodati corrispondano al formato del file esistente.  
  
 Per creare il file nella prima iterazione del ciclo e quindi accodare righe nelle iterazioni successive, è necessario eseguire le operazioni seguenti in fase di progettazione:  
  
1.  Impostare la proprietà WriteOption su **CreateOnce** o **CreateAlways**ed eseguire un'iterazione del ciclo. Il file viene creato e viene garantita così la corrispondenza tra i metadati dei dati accodati e il file.  
  
2.  Reimpostare la proprietà WriteOption su **Append** e impostare la proprietà ValidateExternalMetadata su **False**.  
  
 Se si usa l'opzione **TruncateAppend** invece di **Append** , le righe aggiunte in qualsiasi iterazione precedente verranno troncate e quindi verranno accodate nuove righe. Per usare l'opzione **TruncateAppend** , è anche necessario che i dati corrispondano al formato del file.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Configurazione della destinazione file non elaborato  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate del file non elaborato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Post di blog sugli [aspetti positivi dei file non elaborati](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)nel sito Web sqlservercentral.com.  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>Editor destinazione file non elaborato (pagina Gestione connessione)
  Utilizzare l'Editor destinazione file non elaborato per configurare la destinazione file non elaborato in modo da scrivere dati non elaborati in un file.  
  
 **Per saperne di più**  
  
-   [Aprire l'Editor destinazione file non elaborato](#open)  
  
-   [Impostare le opzioni nella scheda Gestione connessione](#connection)  
  
-   [Impostare le opzioni nella scheda Colonne](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> Aprire l'Editor destinazione file non elaborato  
  
1.  Aggiungere la destinazione file non elaborato in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente e quindi scegliere **Modifica**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Impostare le opzioni nella scheda Gestione connessione  
 **Modalità di accesso**  
 Selezionare come il nome file viene specificato. Selezionare **Nome file** per immettere direttamente il nome file e il percorso o **Nome file da variabile** per specificare una variabile che contiene il nome file.  
  
 **Nome file** o **Nome variabile**  
 Immettere il nome e il percorso del file non elaborato o selezionare la variabile contenente il nome file.  
  
 **Opzione scrittura**  
 Selezionare il metodo utilizzato per creare e scrivere nel file.  
  
 **Generare file non elaborato iniziale**  
 Fare clic sul pulsante per generare un file non elaborato vuoto contenente solo le colonne (file di soli metadati) senza dover eseguire il pacchetto. Nel file sono contenute le colonne selezionate nella pagina **Colonne** di **Editor destinazione file non elaborato**. È possibile puntare l'origine file non elaborato a questo file di soli metadati.  
  
 Quando si fa clic su **Genera file non elaborato iniziale**, viene visualizzata una finestra di messaggio. Fare clic su **OK** per procedere con la creazione del file. Fare clic su **Annulla** per selezionare un elenco diverso di colonne nella pagina **Colonne** .  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> Impostare le opzioni nella scheda Colonne  
 **Colonne di input disponibili**  
 Selezionare uno o più colonne di input per scrivere nel file non elaborato.  
  
 **Colonna di input**  
 Una colonna di input viene aggiunta automaticamente a questa tabella quando la si seleziona in **Colonne di input disponibili**o è possibile selezionare direttamente la colonna di input in questa tabella.  
  
 **Alias di output**  
 Specificare un nome alternativo da utilizzare per la colonna di output.  
  
## <a name="raw-file-destination-editor-columns-page"></a>Editor destinazione file non elaborato (pagina Colonne)
  Utilizzare l'Editor destinazione file non elaborato per configurare la destinazione file non elaborato in modo da scrivere dati non elaborati in un file.  
  
 **Per saperne di più**  
  
-   [Aprire l'Editor destinazione file non elaborato](#open)  
  
-   [Impostare le opzioni nella scheda Gestione connessione](#connection)  
  
-   [Impostare le opzioni nella scheda Colonne](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> Aprire l'Editor destinazione file non elaborato  
  
1.  Aggiungere la destinazione file non elaborato in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente e quindi scegliere **Modifica**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Impostare le opzioni nella scheda Gestione connessione  
 **Modalità di accesso**  
 Selezionare come il nome file viene specificato. Selezionare **Nome file** per immettere direttamente il nome file e il percorso o **Nome file da variabile** per specificare una variabile che contiene il nome file.  
  
 **Nome file** o **Nome variabile**  
 Immettere il nome e il percorso del file non elaborato o selezionare la variabile contenente il nome file.  
  
 **Opzione scrittura**  
 Selezionare il metodo utilizzato per creare e scrivere nel file.  
  
 **Generare file non elaborato iniziale**  
 Fare clic sul pulsante per generare un file non elaborato vuoto contenente solo le colonne (file di soli metadati) senza dover eseguire il pacchetto. È possibile puntare l'origine file non elaborato al file di soli metadati.  
  
 Quando si fa clic sul pulsante, viene visualizzato un elenco delle colonne. È possibile fare clic su Annulla e modificare le colonne o fare clic su OK per procedere con la creazione del file.  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> Impostare le opzioni nella scheda Colonne  
 **Colonne di input disponibili**  
 Selezionare uno o più colonne di input per scrivere nel file non elaborato.  
  
 **Colonna di input**  
 Una colonna di input viene aggiunta automaticamente a questa tabella quando la si seleziona in **Colonne di input disponibili**o è possibile selezionare direttamente la colonna di input in questa tabella.  
  
 **Alias di output**  
 Specificare un nome alternativo da utilizzare per la colonna di output.  
  
## <a name="see-also"></a>Vedere anche  
 [Origine file non elaborato](../../integration-services/data-flow/raw-file-source.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
