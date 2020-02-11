---
title: 'Passaggio 2: Aggiunta e configurazione di una gestione connessione file flat | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c6cd41be722d80baf442db907d6fdab9f334859
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891792"
---
# <a name="step-2-adding-and-configuring-a-flat-file-connection-manager"></a>Passaggio 2: Aggiunta e configurazione di una gestione connessione file flat
  In questa attività si aggiungerà una gestione connessione file flat al pacchetto appena creato. Una gestione connessione file flat abilita un pacchetto all'estrazione di dati da un file flat. Utilizzando tale gestione connessione è possibile specificare il nome file e la posizione, le impostazioni locali e la tabella codici e il formato del file, inclusi i delimitatori di colonna, da applicare quando il pacchetto estrae i dati dal file flat. È anche possibile specificare manualmente il tipo di dati per le singole colonne o usare la finestra di dialogo **Suggerisci tipo di colonne** per eseguire automaticamente il mapping delle colonne di dati estratti ai tipi di dati di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 È necessario creare una nuova gestione connessione file flat per ogni formato di file da utilizzare. Dal momento che in questa esercitazione viene eseguita l'estrazione di dati da più file flat con lo stesso formato di dati, è necessario aggiungere e configurare una sola gestione connessione file flat al pacchetto.  
  
 Per questa esercitazione si configureranno le seguenti proprietà nella gestione connessione file flat:  
  
-   **Nomi delle colonne:** Poiché il file flat non ha nomi di colonna, la gestione connessione file flat crea nomi di colonna predefiniti. Questi nomi predefiniti non sono utili per identificare i dati rappresentati da ogni colonna. Per rendere questi nomi predefiniti più utili, è necessario modificarli in nomi che corrispondano alla tabella dei fatti in cui i dati dei file flat devono essere caricati.  
  
-   **Mapping dei dati:** I mapping dei tipi di dati specificati per la gestione connessione file flat verranno utilizzati da tutti i componenti dell'origine dati file flat che fanno riferimento alla gestione connessione. È possibile eseguire manualmente il mapping dei tipi di dati usando la gestione connessione file flat oppure usare la finestra di dialogo **Suggerisci tipi di colonne** . In questa esercitazione verranno visualizzati i mapping suggeriti nella finestra di dialogo **Suggerisci tipi di colonne** e quindi verranno effettuati manualmente i mapping necessari nella finestra di dialogo **Editor gestione connessione file flat** .  
  
 Gestione connessione file flat fornisce informazioni sulle impostazioni locali per il file di dati. Se il computer non è configurato per l'utilizzo dell'opzione Regional (lingua inglese) (Stati Uniti), è necessario impostare proprietà aggiuntive nella finestra di dialogo **Editor gestione connessione file flat** .  
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>Per aggiungere una gestione connessione file flat al pacchetto SSIS.  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dell'area **Gestioni connessioni** e quindi fare clic su **Nuova connessione file flat**.  
  
2.  Nella finestra di dialogo **Editor gestione connessione file flat** , per **Nome gestione connessione**, digitare **Sample Flat File Source Data**.  
  
3.  Fare clic su **Sfoglia**.  
  
4.  Nella finestra di dialogo **Apri** individuare il file SampleCurrencyData.txt nel computer.  
  
     I dati di esempio sono inclusi nei pacchetti di lezioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per scaricare i dati di esempio e i pacchetti di lezioni, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **Downloads** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Deselezionare i nomi di colonna nella prima casella di controllo della riga di dati.  
  
### <a name="to-set-locale-sensitive-properties"></a>Per impostare le proprietà dipendenti dalle impostazioni locali  
  
1.  Nella finestra di dialogo **Editor gestione connessione file flat** fare clic su **Generale**.  
  
2.  Impostare **impostazioni locali** su inglese (Stati Uniti) e **tabella codici** su 1252.  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>Per rinominare le colonne nella gestione connessione file flat  
  
1.  Nella finestra di dialogo **Editor gestione connessione file flat** fare clic su **Avanzate**.  
  
2.  Nel riquadro delle proprietà apportare le seguenti modifiche:  
  
    -   Modificare la proprietà nome **colonna 0** in `AverageRate`.  
  
    -   Modificare la proprietà nome **colonna 1** in `CurrencyID`.  
  
    -   Modificare la proprietà nome **colonna 2** in `CurrencyDate`.  
  
    -   Modificare la proprietà nome **colonna 3** in `EndOfDayRate`.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, le quattro colonne sono inizialmente impostate su un tipo di dati stringa [DT_STR] con un valore `OutputColumnWidth` di 50.  
  
### <a name="to-remap-column-data-types"></a>Per modificare il mapping dei tipi di dati di colonna  
  
1.  Nella finestra di dialogo **Editor gestione connessione file flat** fare clic su **Suggerisci tipi**.  
  
     
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] indica automaticamente i tipi di dati più appropriati in base alle prime 200 righe di dati. È inoltre possibile modificare le opzioni suggerite in modo da campionare più o meno dati, specificare il tipo di dati predefinito per numeri interi o dati booleani oppure aggiungere spazi come spaziatura interna nelle colonne stringa.  
  
     Per il momento non apportare modifiche alle opzioni nella finestra di dialogo **Suggerisci tipi di colonne** e fare clic su **OK** in modo che [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] suggerisca i tipi di dati per le colonne. In questo modo verrà nuovamente visualizzato il riquadro **Avanzate** della finestra di dialogo **Editor gestione connessione file flat** in cui è possibile visualizzare i tipi di dati delle colonne suggeriti da [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se si fa clic su **Annulla**non verranno indicati suggerimenti relativi ai metadati delle colonne e verrà usato il tipo di dati string predefinito, ovvero DT_STR.  
  
     In questa esercitazione, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] suggerisce i tipi di dati mostrati nella seconda colonna della tabella seguente per i dati ricavati dal file SampleCurrencyData.txt. Tuttavia, i tipi di dati necessari per le colonne nella destinazione, che verranno definiti in una fase successiva, sono mostrati nell'ultima colonna della tabella che segue.  
  
    |Colonna file flat|Tipo suggerito|Colonna di destinazione|Tipo destinazione|  
    |----------------------|--------------------|------------------------|----------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|float|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|Data|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|float|  
  
     Il tipo di dati suggerito per `CurrencyID` la colonna non è compatibile con il tipo di dati del campo nella tabella di destinazione. Poiché il tipo di dati `DimCurrency.CurrencyAlternateKey` di è nchar (3) `CurrencyID` , deve essere modificato da String [DT_STR] a String [DT_WSTR]. Inoltre, il campo `DimDate.FullDateAlternateKey` viene definito come tipo di dati Data; Pertanto, `CurrencyDate` deve essere modificato da date [DT_DATE] a data del database [DT_DBDATE].  
  
2.  Nell'elenco selezionare la colonna CurrencyID e nel riquadro delle proprietà modificare il tipo di dati della colonna `CurrencyID` da string [DT_STR] alla stringa Unicode [DT_WSTR].  
  
3.  Nel riquadro delle proprietà modificare il tipo di dati della colonna `CurrencyDate` da date [DT_DATE] a database date [DT_DBDATE].  
  
4.  Fare clic su **OK**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 3: Aggiunta e configurazione di una gestione connessione OLE DB](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione connessione file flat](connection-manager/file-connection-manager.md)   
 [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md)  
  
  
