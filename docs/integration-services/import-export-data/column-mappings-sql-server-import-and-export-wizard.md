---
title: Mapping colonne (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f7b30970020963e83fa101971d6c30d9e76397a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723947"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Mapping colonne (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Dopo aver selezionato le tabelle e le viste esistenti per copiare o rivedere la query fornita, fare clic su **Modifica mapping**per consentire a Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di visualizzare la finestra di dialogo **Mapping colonne** . In questa pagina è necessario specificare e configurare le colonne di destinazione per ricevere i dati copiati dalle colonne di origine. Spesso non è necessario apportare modifiche in questa pagina.
  
Se non si vuole copiare tutte le colonne della tabella selezionata, è possibile escludere in questa pagina le colonne non necessarie. Selezionare **Ignora** nella colonna **Destinazione** dell'elenco **Mapping** per le colonne che non si desidera copiare.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Screenshot della pagina Mapping colonne 
 Lo screenshot seguente riporta un esempio della finestra di dialogo **Mapping colonne** della procedura guidata. 
 
 In questo esempio, notare come la procedura guidata creerà una nuova tabella di destinazione perché è stato selezionato **Crea tabella di destinazione** . Per impostazione predefinita, la procedura guidata assegna a ogni colonna della nuova tabella di destinazione lo stesso nome e tipo di dati e le stesse proprietà della colonna di origine corrispondente. 
  
 ![Pagina Mapping colonne dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/media/column-mappings.png "Pagina Mapping colonne dell'Importazione/Esportazione guidata")  
  
## <a name="review-the-source-and-destination"></a>Esaminare l'origine e la destinazione 
![Pagina Mapping colonne, sezione origine e destinazione](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Origine**  
 La tabella, la vista o la query di origine selezionata.  
  
 **Destinazione**  
 La tabella o la vista di destinazione selezionata.  

## <a name="optionally-create-a-new-destination-table"></a>Creare una nuova tabella di destinazione (facoltativo)
![Pagina Mapping colonne, sezione nuova tabella](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Crea tabella di destinazione/file**  
 Creare la tabella di destinazione se non esiste già.    
  
 **Modifica codice SQL**  
Fare clic su **Modifica SQL** per aprire la finestra di dialogo **Istruzione SQL CREATE TABLE** . Usare l'istruzione CREATE TABLE generata automaticamente o modificarla in base alle proprie esigenze. Se si modifica questa istruzione manualmente, è necessario assicurarsi che l'elenco dei mapping delle colonne riconosca le modifiche. Per altre informazioni, vedere [Istruzione SQL CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>Talvolta queste opzioni sono disabilitate
L'opzione **Crea tabella/file di destinazione** e il pulsante **Modifica codice SQL** vengono abilitati o disabilitati automaticamente.

-   **Abilitati.** Se è stata specificata una **nuova** tabella di destinazione nella pagina **Seleziona tabelle e viste di origine**, l'opzione **Crea tabella di destinazione** viene automaticamente selezionata e il pulsante **Modifica codice SQL** viene abilitato.

-   **Disabilitati.** Se è stata selezionata una tabella di destinazione **esistente** nella pagina **Seleziona tabelle e viste di origine**, l'opzione **Crea tabella di destinazione** e il pulsante **Modifica codice SQL** sono disabilitati. Per creare una nuova tabella di destinazione tornare alla pagina **Seleziona tabelle e viste di origine** e immettere il nome di una **nuova** tabella nella colonna **Destinazione**.  

## <a name="what-about-existing-data-in-the-destination"></a>Opzioni per i dati esistenti nella destinazione
![Pagina Mapping colonne, sezione opzioni](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Elimina righe nella tabella di destinazione/file**  
 Consente di specificare se cancellare i dati da una tabella esistente prima di caricare nuovi dati.  
  
 **Aggiungi righe alla tabella di destinazione/file**  
 Consente di specificare se aggiungere nuovi dati a quelli già presenti in una tabella esistente.  
  
 **Elimina e ricrea tabella di destinazione**  
 Selezionare questa opzione per sovrascrivere la tabella di destinazione. Questa opzione è disponibile solo quando è stata usata la procedura guidata per creare la tabella di destinazione. La tabella di destinazione viene eliminata e ricreata solo se si salva il pacchetto creato dalla procedura guidata e quindi lo si esegue nuovamente. Questa opzione è utile per testare le impostazioni più volte.
  
 **Consenti IDENTITY_INSERT**  
 Selezionare questa opzione per consentire l'inserimento dei valori di identità esistenti nei dati di origine all'interno di una colonna Identity della tabella di destinazione. Per impostazione predefinita, generalmente non è possibile applicare questa opzione alla colonna Identity di destinazione.  
  
> [!TIP]
> Se le chiavi primarie esistenti si trovano in una colonna Identity, in una contatore o nell'equivalente, in genere è necessario selezionare questa opzione per mantenere i valori di chiave primaria esistenti.  In caso contrario la colonna Identity di destinazione assegna in genere nuovi valori.  

## <a name="keep-your-autonumber-or-identity-values"></a>Mantenere i valori di numerazione automatica o Identity
Se si sta esportando dati per i quali è presente una colonna di numerazione automatica o una colonna Identity, ad esempio se si sta esportando dati da Microsoft Access, selezionare **Consenti IDENTITY_INSERT** come appena descritto.

## <a name="review-column-mappings"></a>Esaminare i mapping delle colonne
![Pagina Mapping colonne, sezione mapping](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Mapping**  
 Consente di visualizzare la modalità di mapping tra ogni colonna nell'origine dati e una colonna nella destinazione.
 
L'elenco **Mapping** contiene le colonne seguenti.  
  
-    **Origine**  
     Consente di visualizzare ogni colonna di origine.  
  
-   **Destinazione**  
    Visualizzare la colonna di destinazione mappata o selezionare una colonna diversa.
    
    Non è necessario copiare tutte le colonne dalla tabella di origine. Selezionare **Ignora** per le colonne che si desidera ignorare. Prima di eseguire il mapping delle colonne, è necessario ignorare tutte le colonne di cui non verrà eseguito il mapping.  
  
-   **Tipo**  
    Visualizzare il tipo di dati per la colonna di destinazione o selezionare un tipo di dati diverso.
  
-   **Ammette i valori Null**  
    Consente di specificare se la colonna di destinazione ammette valori Null.  
  
-   **Dimensione**  
    Specificare il numero di caratteri nella colonna di destinazione, se applicabile.  
  
-    **Precisione**  
    Specificare la precisione dei dati numerici nella colonna di destinazione, ovvero il numero di cifre, se applicabile.  
  
 -   **Scala**  
    Specificare la scala dei dati numerici nella colonna di destinazione, ovvero il numero di cifre decimali, se applicabile.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?  
 Dopo aver esaminato e configurato le colonne di destinazione per ricevere i dati copiati dalle colonne di origine e aver fatto clic su **OK** sarà possibile passare dalla finestra di dialogo **Mapping colonne** alla pagina **Seleziona tabelle e viste di origine** o alla pagina **Configurare la destinazione del file flat**. Per altre informazioni, vedere [Seleziona tabelle e viste di origine](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurare la destinazione del file flat](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Se nell'elenco **Mapping** è stato specificato un mapping che potrebbe non avvenire con successo, la finestra di dialogo **Mapping colonne** riporta alla pagina **Verifica mapping tra i tipi di dati** . In questa pagina, esaminare gli avvisi, specificare le opzioni di conversione e anche come gestire gli errori. Per altre informazioni, vedere [Verifica mapping tra i tipi di dati](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vedere anche
[Mapping dei tipi di dati nell'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Iniziare con questo semplice esempio dell'Importazione/Esportazione guidata](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

