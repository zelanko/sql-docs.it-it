---
title: Creare la struttura di Data Mining (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures, creating
ms.assetid: b8b1eedc-4d6d-4429-a578-e629ec573934
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae5244110e6b95434f9008fd7dc99cee259acf8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086822"
---
# <a name="create-mining-structure-sql-server-data-mining-add-ins"></a>Crea struttura di data mining (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Crea struttura di Data Mining, barra multifunzione Data Mining](media/dmc-createstruct.gif "pulsante Crea struttura di Data Mining, barra multifunzione Data Mining")  
  
 Usare la **avanzate** opzione il **modellazione dati** quando si desidera creare un set di dati utilizzato per l'analisi senza necessariamente creare un modello di gruppo. Ciò risulta utile quando si desidera provare a utilizzare algoritmi diversi.  
  
 Dopo aver creato la struttura di data mining, utilizzare il [aggiunta modello a struttura](add-model-to-structure-data-mining-add-ins-for-excel.md) procedura guidata per creare un modello basato su tale struttura. È anche possibile creare nuovi modelli utilizzando il **Editor avanzato Data Mining Query**.  
  
 Questa opzione può essere utilizzata anche quando si desidera compilare modelli con uno degli algoritmi avanzati, supportati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ma non disponibili tramite una procedura guidata, ad esempio la regressione lineare o Sequence Clustering o se si utilizza un algoritmo personalizzato.  
  
> [!NOTE]  
>  Quando si crea la struttura di data mining, è inoltre possibile stabilire un set di dati di test selezionato casualmente che può essere utilizzato per convalidare tutti i modelli. Questa soluzione è pratica perché è possibile confrontare facilmente l'accuratezza di un modello rispetto a un set di dati comune. Selezionare l'opzione **suddividere i dati in set di training e set di testing** e specificare una percentuale appropriata di dati da riservare al test, in genere circa il 30 percento.  
  
## <a name="use-the-wizard-to-create-a-mining-structure"></a>Utilizzare la procedura guidata per creare una struttura di data mining  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **Advanced**e selezionare **Create Structure**.  
  
2.  Nel **selezione dati di origine** finestra di dialogo, specificare l'intervallo di Excel, una tabella dati di Excel o origine dati esterna che contiene i dati da usare per l'analisi.  
  
     Scegliere **Avanti**.  
  
3.  Nel **Seleziona colonne** dialogo casella, esaminare l'elenco di colonne disponibili nell'origine dati selezionata.  
  
4.  Fare clic sulla freccia a destra del nome della colonna per modificare la **utilizzo** della colonna, scegliendo tra i valori:  
  
    -   **Key**. A ogni modello deve essere associata almeno una chiave.  
  
    -   **Chiave temporale**. Questa opzione è disponibile solo per i modelli di previsione, laddove richiesto.  
  
    -   **Includere**. Indica che la colonna deve essere resa disponibile nella struttura di data mining ma non è una colonna chiave.  
  
    -   **Non usare**. Indica che la colonna non deve essere inclusa nella struttura di data mining.  
  
     Si tenga presente che è sempre possibile ignorare le colonne quando si compila il modello, mentre per aggiungerne altre in un secondo momento è necessario rielaborare la struttura e il modello.  
  
5.  Fare clic su Sfoglia **(...)**  pulsante per impostare il tipo di contenuto, tipo di dati e i flag di modellazione.  
  
    > [!NOTE]  
    >  Se nella colonna sono contenuti dati numerici, è necessario aprire sempre questa finestra di dialogo per assicurarsi che sia stato scelto il tipo di dati corretto. In alcuni casi, anche se i dati di input sono numeri, è opportuno considerarli come variabili di categoria o valori discreti, anziché numeri continui.  
    >   
    >  Una colonna relativa al codice postale potrebbe ad esempio essere elencata per impostazione predefinita come tipo di dati Long continuo, ma per ottenere risultati migliori, è possibile specificare che venga gestita come valore di testo discreto.  
    >   
    >  Per altre informazioni, vedere la sezione sui tipi di contenuto in [scelta dei dati per Data Mining](choosing-data-for-data-mining.md).  
  
     Scegliere **OK** per chiudere la finestra di dialogo.  
  
6.  Scegliere **Avanti**.  
  
     A seconda del tipo di dati utilizzato, potrebbe essere necessario completare la procedura guidata dopo questo passaggio. In tal caso, passare direttamente alla sezione di **fine** pagina per nome alla struttura di data mining.  
  
     Per altri modelli, si dispone dell'opzione aggiuntiva per creare un set di dati di test.  
  
7.  Nel **suddividere i dati in set di training e set di dati di testing** finestra di dialogo, specificare come si desidera partizionare i dati. Per impostazione predefinita, il 30% dei dati viene utilizzato per il testing.  
  
     È possibile digitare il numero massimo di righe da utilizzare per il testing.  
  
     Scegliere **Avanti**.  
  
8.  Nel **fine** finestra di dialogo digitare un nome e una descrizione per la nuova struttura di data mining.  
  
9. Scegliere **Fine**.  
  
### <a name="related-options"></a>Opzioni correlate  
  
|Opzione|Commenti|  
|------------|--------------|  
|**Selezionare i dati di origine** nella finestra di dialogo|Quando si seleziona una tabella di Excel, è necessario indicare se ai dati sono già associate intestazioni. Se si ignora questa operazione, la prima riga di dati verrà utilizzata come nome di colonna.<br /><br /> Se si usa l'opzione **origine dati esterna**, è possibile usare qualsiasi tipo di dati che possono essere definiti in un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zdroj dat. Tuttavia, nella finestra di dialogo del componente aggiuntivo per la creazione di nuove origini dati non è incluso l'intervallo completo di origini dati supportate da Analysis Services. È pertanto consigliabile creare in anticipo le origini dati nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e, successivamente, connettersi utilizzando i componenti aggiuntivi.|  
|**Editor Query origine dati** nella finestra di dialogo|Dopo aver stabilito la connessione all'origine dati specificata, è possibile aggiungere colonne o creare una query personalizzata per generare colonne personalizzate.|  
|**Suddividere i dati in set di training e set di dati di testing**|Un valore consigliato per il training e set di testing è 70% per il training e il 30% per il test; Tuttavia, se si dispone di una grande quantità di dati, è possibile specificare un numero massimo di righe per il testing.|  
|Finestra di dialogo Fine|Le opzioni per il drill-through sono disponibili in alcuni tipi di modello e sono molto utili se sono state incluse colonne di dettagli nella struttura di data mining. Ad esempio, se si crea un modello di clustering, è possibile includere dettagli quali il nome o l'indirizzo di posta elettronica per il drill-through ma non l'analisi, per semplificare l'operazione per contattare i clienti in un determinato cluster.|  
  
###  <a name="Bkmk_strctcolumn"></a> Impostazione utilizzo colonne nella creazione guidata di struttura di Data Mining  
 Quando si crea una nuova struttura di data mining, è possibile specificare quali colonne dell'origine dati devono essere incluse nella struttura e come verranno utilizzate tali colonne. Tenere presente che una struttura di data mining può supportare più modelli di data mining.  
  
|Valori|Descrizione|  
|------------|-----------------|  
|**Include**|Consente di specificare che la colonna contiene dati utilizzabili per l'analisi o per la stima.|  
|**Key**|Consente di specificare che nella colonna è contenuto un ID transazione, un ID serie o un'altra chiave necessaria per l'elaborazione.<br /><br /> Tutti gli algoritmi richiedono una colonna Chiave. Con alcuni algoritmi è tuttavia consentita una sola chiave, mentre con altri sono consentite più chiavi.<br /><br /> Se la colonna contiene una chiave ma non è necessaria per l'elaborazione, selezionare **non si usano**.|  
|**Chiave temporale**|Consente di specificare che la colonna contiene una data o un altro valore numerico utilizzabile per identificare in modo univoco gli elementi di una serie temporale.|  
|**Non usare**|Consente di specificare che la colonna deve essere ignorata. I dati contenuti nella colonna non verranno elaborati.|  
  
 Per elaborare correttamente un modello, è necessario indicare all'algoritmo la colonna chiave che identifica univocamente ogni riga, la colonna di destinazione per la creazione delle stime, se si sta creando un modello stimabile e le colonne da utilizzare come colonne di input per creare le relazioni che consentono di stimare la colonna di destinazione.  
  
-   Le colonne specificate come **non usare** non saranno presenti nella struttura di data mining.  
  
     L'aggiunta di colonne non necessarie o la presenza di valori errati può influire negativamente sui risultati dell'analisi. Assicurarsi pertanto di includere solo le colonne pertinenti. Ricordare, tuttavia, che le colonne non utilizzate nella struttura di data mining non saranno disponibili per le query.  
  
-   Le colonne specificate come le **inclusione** tipo verranno inclusi nella struttura di data mining e potranno essere utilizzata successivamente per l'analisi o la stima nei modelli di data mining.  
  
     Se non si è certi di utilizzare la colonna, è sempre possibile includerla nella struttura di data mining e quindi creare un modello di data mining in cui non viene utilizzata. È ad esempio possibile includere nei dati una colonna per il numero di telefono per riferimento futuro, ma creare un modello di clustering in cui i numeri di telefono vengono ignorati. Dopo aver creato i cluster, è possibile creare una query che restituisce i numeri di telefono delle persone appartenenti a un cluster specifico.  
  
-   Tutti gli algoritmi richiedono una **chiave** colonna. I valori della colonna Chiave devono essere univoci. Oggetto **Key Time** colonna è rappresentata dai modelli necessaria solo per la previsione o time series. .  
  
### <a name="requirements"></a>Requisiti  
 Per creare una struttura di data mining, è necessario disporre di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È necessaria una connessione anche se si utilizzano strutture temporanee. Per altre informazioni su come creare o modificare una connessione, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
