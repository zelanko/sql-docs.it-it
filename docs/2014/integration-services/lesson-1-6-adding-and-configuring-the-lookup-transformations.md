---
title: 'Passaggio 6: Aggiunta e configurazione delle trasformazioni Ricerca | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f652519efc4b77bd785cdded468fe114f6499200
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62891549"
---
# <a name="step-6-adding-and-configuring-the-lookup-transformations"></a>Passaggio 6: Aggiunta e configurazione delle trasformazioni Ricerca
  Dopo aver configurato l'origine file flat per l'estrazione di dati dal file di origine si definiranno le trasformazioni Ricerca necessarie per ottenere i valori di **CurrencyKey** e **DateKey**. Una trasformazione Ricerca esegue una ricerca tramite l'unione in join dei dati della colonna di input specificata con una colonna di un set di dati di riferimento. Il set di dati di riferimento può essere una vista o tabella esistente, una nuova tabella o il risultato di un'istruzione SQL. In questa esercitazione, la trasformazione Ricerca utilizza una gestione connessione OLE DB per connettersi al database che contiene i dati che costituiscono l'origine del set di dati di riferimento.  
  
> [!NOTE]  
>  È anche possibile configurare la trasformazione Ricerca per collegarsi a una cache che contiene il set di dati di riferimento. Per altre informazioni, vedere [trasformazione Ricerca](data-flow/transformations/lookup-transformation.md).  
  
 In questa esercitazione verranno aggiunti al pacchetto e configurati i due componenti di trasformazione Ricerca seguenti:  
  
-   Una trasformazione per eseguire la ricerca di valori della colonna **CurrencyKey** della tabella delle dimensioni **DimCurrency** in base alla corrispondenza con i valori della colonna **CurrencyID** del file flat.  
  
-   Una trasformazione per eseguire una ricerca di valori della colonna **DateKey** della tabella delle dimensioni **DimDate** in base alla corrispondenza con i valori della colonna **CurrencyDate** del file flat.  
  
 In entrambi i casi nella trasformazione Ricerca verrà utilizzata la gestione connessione OLE DB creata in precedenza.  
  
### <a name="to-add-and-configure-the-lookup-currency-key-transformation"></a>Per aggiungere e configurare la trasformazione Lookup Currency Key  
  
1.  Nella **casella degli strumenti SSIS**espandere **comune**, quindi trascinare **ricerca** sull'area di progettazione della scheda **flusso di dati** . Posizionare la ricerca direttamente sotto l'origine **dati Estrai valuta di esempio** .  
  
2.  Fare clic sull'origine del file flat **Extract Sample Currency Data** e trascinare la freccia verde sulla trasformazione **Ricerca** appena aggiunta per collegare i due componenti.  
  
3.  Nell'area di progettazione **Flusso di dati** fare clic su **Ricerca** nella trasformazione **Ricerca** e cambiare il nome in **Lookup Currency Key**.  
  
4.  Fare doppio clic sulla trasformazione **Lookup Currency Key** per visualizzare l'Editor trasformazione Ricerca.  
  
5.  Nella pagina **Generale** effettuare le selezioni seguenti:  
  
    1.  Selezionare **Full cache**.  
  
    2.  Nell'area **Tipo di connessione** selezionare **Gestione connessione OLE DB**.  
  
6.  Nella pagina **Connessione** effettuare le selezioni seguenti:  
  
    1.  Nella finestra di dialogo **Gestione connessione OLE DB** assicurarsi che sia visualizzato **localhost.AdventureWorksDW2012** .  
  
    2.  Selezionare **Usa i risultati di una query SQL**, quindi digitare o copiare l'istruzione SQL seguente:  
  
        ```  
        select * from (select * from [dbo].[DimCurrency]) as refTable  
        where [refTable].[CurrencyAlternateKey] = 'ARS'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'AUD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'BRL'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CAD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CNY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'DEM'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'EUR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'FRF'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'GBP'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'JPY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'MXN'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'SAR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'USD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'VEB'  
        ```  
  
7.  Nella pagina **Colonne** effettuare le selezioni seguenti:  
  
    1.  Nel pannello **Colonne di input disponibili** trascinare **CurrencyID** sul pannello **Colonne di ricerca disponibili** e rilasciarlo su **CurrencyAlternateKey**.  
  
    2.  Nell'elenco **Colonne di ricerca disponibili** selezionare la casella di controllo a sinistra di **CurrencyKey**.  
  
8.  Fare clic su **OK** per tornare all'area di progettazione **Flusso di dati** .  
  
9. Fare clic con il pulsante destro del mouse sulla trasformazione Lookup Currency Key e scegliere **Proprietà**.  
  
10. `LocaleID` Nella finestra Proprietà verificare che la proprietà sia impostata su **inglese (Stati Uniti)** e che la proprietà **DefaultCodePage** sia impostata su **1252**.  
  
### <a name="to-add-and-configure-the--lookup-datekey-transformation"></a>Per aggiungere e configurare la trasformazione Lookup DateKey  
  
1.  Nella **Casella degli strumenti SSIS**trascinare **Ricerca** sull'area di progettazione **Flusso di dati** . Posizionare Ricerca proprio sotto la trasformazione **Lookup Currency Key** .  
  
2.  Fare clic sulla trasformazione **Lookup Currency Key** e trascinare la freccia verde sulla nuova trasformazione **Ricerca** per collegare i due componenti.  
  
3.  Nella finestra di dialogo **Selezione input e output** fare clic su **Output corrispondenza ricerca** nella casella di riepilogo **Output** e fare clic su **OK**.  
  
4.  Nell'area di progettazione **Flusso di dati** fare clic su **Ricerca** nella trasformazione **Ricerca** appena aggiunta e impostare il nome su **Lookup Date Key**.  
  
5.  Fare doppio clic sulla trasformazione **Lookup Date Key** .  
  
6.  Nella pagina **Generale** selezionare **Partial cache**.  
  
7.  Nella pagina **Connessione** effettuare le selezioni seguenti:  
  
    1.  Nella finestra di dialogo **Gestione connessione OLE DB** assicurarsi che sia visualizzato **localhost.AdventureWorksDW2012** .  
  
    2.  Nella casella **Usa una tabella o una vista** digitare o selezionare **[dbo].[DimDate]**.  
  
8.  Nella pagina **Colonne** effettuare le selezioni seguenti:  
  
    1.  Nel pannello **Colonne di input disponibili** trascinare **CurrencyDate** sul pannello **Colonne di ricerca disponibili** e rilasciarlo su **FullDateAlternateKey**.  
  
    2.  Nell'elenco **Colonne di ricerca disponibili** selezionare la casella di controllo a sinistra di **DateKey**.  
  
9. Nella pagina **Avanzate** rivedere le opzioni di memorizzazione nella cache.  
  
10. Fare clic su **OK** per tornare all'area di progettazione **Flusso di dati** .  
  
11. Fare clic con il pulsante destro del mouse sulla trasformazione Lookup Date Key e scegliere **Proprietà.**  
  
12. `LocaleID` Nella finestra Proprietà verificare che la proprietà sia impostata su **inglese (Stati Uniti)** e che la proprietà **DefaultCodePage** sia impostata su **1252**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 7: Aggiunta e configurazione della destinazione OLE DB](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Trasformazione Ricerca](data-flow/transformations/lookup-transformation.md)  
  
  
