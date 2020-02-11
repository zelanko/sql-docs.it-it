---
title: Creare una struttura di data mining (SQL Server componenti aggiuntivi Data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086822"
---
# <a name="create-mining-structure-sql-server-data-mining-add-ins"></a>Crea struttura di data mining (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Crea la struttura di data mining, barra multifunzione Data mining](media/dmc-createstruct.gif "Pulsante Crea la struttura di data mining, barra multifunzione Data mining")  
  
 Utilizzare l'opzione **Avanzate** nel gruppo **modellazione dati** quando si desidera creare un set di dati utilizzato per l'analisi senza necessariamente creare un modello. Ciò risulta utile quando si desidera provare a utilizzare algoritmi diversi.  
  
 Dopo aver creato la struttura di data mining, utilizzare la procedura guidata [Aggiungi modello a struttura](add-model-to-structure-data-mining-add-ins-for-excel.md) per creare un modello basato su tale struttura. È inoltre possibile creare nuovi modelli utilizzando l' **Editor avanzato query di data mining**.  
  
 Questa opzione può essere utilizzata anche quando si desidera compilare modelli con uno degli algoritmi avanzati, supportati da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ma non disponibili tramite una procedura guidata, ad esempio la regressione lineare o Sequence Clustering o se si utilizza un algoritmo personalizzato.  
  
> [!NOTE]  
>  Quando si crea la struttura di data mining, è inoltre possibile stabilire un set di dati di test selezionato casualmente che può essere utilizzato per convalidare tutti i modelli. Questa soluzione è pratica perché è possibile confrontare facilmente l'accuratezza di un modello rispetto a un set di dati comune. È sufficiente selezionare l'opzione **suddividere i dati in set di training e di testing** e specificare una percentuale appropriata di dati da riservare per il test, in genere circa il 30%.  
  
## <a name="use-the-wizard-to-create-a-mining-structure"></a>Utilizzare la procedura guidata per creare una struttura di data mining  
  
1.  Sulla barra multifunzione **data mining** fare clic su **Avanzate**e selezionare **crea struttura**.  
  
2.  Nella finestra di dialogo **selezione dati di origine** specificare l'intervallo di Excel, la tabella dati di Excel o l'origine dati esterna che contiene i dati che si desidera utilizzare per l'analisi.  
  
     Fare clic su **Avanti**.  
  
3.  Nella finestra di dialogo **Seleziona colonne** esaminare l'elenco delle colonne disponibili nell'origine dati selezionata.  
  
4.  Fare clic sulla freccia a destra del nome della colonna per modificare l' **utilizzo** della colonna, scegliendo tra i valori seguenti:  
  
    -   **Chiave**. A ogni modello deve essere associata almeno una chiave.  
  
    -   **Chiave temporale**. Questa opzione è disponibile solo per i modelli di previsione, laddove richiesto.  
  
    -   **Includi**. Indica che la colonna deve essere resa disponibile nella struttura di data mining ma non è una colonna chiave.  
  
    -   Non **usare**. Indica che la colonna non deve essere inclusa nella struttura di data mining.  
  
     Si tenga presente che è sempre possibile ignorare le colonne quando si compila il modello, mentre per aggiungerne altre in un secondo momento è necessario rielaborare la struttura e il modello.  
  
5.  Fare clic sul pulsante Sfoglia **(...)** per impostare il tipo di contenuto, il tipo di dati e i flag di modellazione.  
  
    > [!NOTE]  
    >  Se nella colonna sono contenuti dati numerici, è necessario aprire sempre questa finestra di dialogo per assicurarsi che sia stato scelto il tipo di dati corretto. In alcuni casi, anche se i dati di input sono numeri, è opportuno considerarli come variabili di categoria o valori discreti, anziché numeri continui.  
    >   
    >  Una colonna relativa al codice postale potrebbe ad esempio essere elencata per impostazione predefinita come tipo di dati Long continuo, ma per ottenere risultati migliori, è possibile specificare che venga gestita come valore di testo discreto.  
    >   
    >  Per ulteriori informazioni, vedere la sezione relativa ai tipi di contenuto nella [scelta dei dati per il data mining](choosing-data-for-data-mining.md).  
  
     Scegliere **OK** per chiudere la finestra di dialogo.  
  
6.  Fare clic su **Avanti**.  
  
     A seconda del tipo di dati utilizzato, potrebbe essere necessario completare la procedura guidata dopo questo passaggio. In tal caso, passare alla pagina **Finish (fine** ) per assegnare un nome alla struttura di data mining.  
  
     Per altri modelli, si dispone dell'opzione aggiuntiva per creare un set di dati di test.  
  
7.  Nella finestra di dialogo **suddividere i dati in set di dati di training e di testing** specificare il modo in cui si desidera partizionare i dati. Per impostazione predefinita, il 30% dei dati viene utilizzato per il testing.  
  
     È possibile digitare il numero massimo di righe da utilizzare per il testing.  
  
     Fare clic su **Avanti**.  
  
8.  Nella finestra di dialogo **fine** Digitare un nome e una descrizione per la nuova struttura di data mining.  
  
9. Fare clic su **Fine**.  
  
### <a name="related-options"></a>Opzioni correlate  
  
|Opzione|Commenti|  
|------------|--------------|  
|Finestra di dialogo **selezione dati di origine**|Quando si seleziona una tabella di Excel, è necessario indicare se ai dati sono già associate intestazioni. Se si ignora questa operazione, la prima riga di dati verrà utilizzata come nome di colonna.<br /><br /> Se si utilizza l'opzione **origine dati esterna**, è possibile utilizzare qualsiasi tipo di dati che può essere definito in un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] origine dati. Tuttavia, nella finestra di dialogo del componente aggiuntivo per la creazione di nuove origini dati non è incluso l'intervallo completo di origini dati supportate da Analysis Services. È pertanto consigliabile creare in anticipo le origini dati nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e, successivamente, connettersi utilizzando i componenti aggiuntivi.|  
|Finestra di dialogo **Editor query origine dati**|Dopo aver stabilito la connessione all'origine dati specificata, è possibile aggiungere colonne o creare una query personalizzata per generare colonne personalizzate.|  
|**Divisione dei dati in set di training e in set di testing**|Un valore consigliato per training e set di testing è il 70% per il training e il 30% per il testing; Tuttavia, se si dispone di una grande quantità di dati, è possibile specificare un numero massimo di righe per il test.|  
|Finestra di dialogo Fine|Le opzioni per il drill-through sono disponibili in alcuni tipi di modello e sono molto utili se sono state incluse colonne di dettagli nella struttura di data mining. Ad esempio, se si crea un modello di clustering, è possibile includere dettagli quali il nome o l'indirizzo di posta elettronica per il drill-through ma non l'analisi, per semplificare l'operazione per contattare i clienti in un determinato cluster.|  
  
###  <a name="Bkmk_strctcolumn"></a>Impostazione dell'utilizzo delle colonne nella procedura guidata crea struttura di data mining  
 Quando si crea una nuova struttura di data mining, è possibile specificare quali colonne dell'origine dati devono essere incluse nella struttura e come verranno utilizzate tali colonne. Tenere presente che una struttura di data mining può supportare più modelli di data mining.  
  
|Valori|Descrizione|  
|------------|-----------------|  
|**Includere**|Consente di specificare che la colonna contiene dati utilizzabili per l'analisi o per la stima.|  
|**Chiave**|Consente di specificare che nella colonna è contenuto un ID transazione, un ID serie o un'altra chiave necessaria per l'elaborazione.<br /><br /> Tutti gli algoritmi richiedono una colonna Chiave. Con alcuni algoritmi è tuttavia consentita una sola chiave, mentre con altri sono consentite più chiavi.<br /><br /> Se la colonna contiene una chiave ma non è necessaria per l'elaborazione, selezionare **non utilizzare**.|  
|**Chiave temporale**|Consente di specificare che la colonna contiene una data o un altro valore numerico utilizzabile per identificare in modo univoco gli elementi di una serie temporale.|  
|**Non usare**|Consente di specificare che la colonna deve essere ignorata. I dati contenuti nella colonna non verranno elaborati.|  
  
 Per elaborare correttamente un modello, è necessario indicare all'algoritmo la colonna chiave che identifica univocamente ogni riga, la colonna di destinazione per la creazione delle stime, se si sta creando un modello stimabile e le colonne da utilizzare come colonne di input per creare le relazioni che consentono di stimare la colonna di destinazione.  
  
-   Le colonne specificate come non **utilizzare** non saranno presenti nella struttura di data mining.  
  
     L'aggiunta di colonne non necessarie o la presenza di valori errati può influire negativamente sui risultati dell'analisi. Assicurarsi pertanto di includere solo le colonne pertinenti. Ricordare, tuttavia, che le colonne non utilizzate nella struttura di data mining non saranno disponibili per le query.  
  
-   Le colonne specificate come tipo di **inclusione** verranno incluse nella struttura di data mining e successivamente potranno essere utilizzate per l'analisi o la stima nei modelli di data mining.  
  
     Se non si è certi di utilizzare la colonna, è sempre possibile includerla nella struttura di data mining e quindi creare un modello di data mining in cui non viene utilizzata. È ad esempio possibile includere nei dati una colonna per il numero di telefono per riferimento futuro, ma creare un modello di clustering in cui i numeri di telefono vengono ignorati. Dopo aver creato i cluster, è possibile creare una query che restituisce i numeri di telefono delle persone appartenenti a un cluster specifico.  
  
-   Tutti gli algoritmi richiedono una colonna **chiave** . I valori della colonna Chiave devono essere univoci. Una colonna **chiave temporale** è obbligatoria solo per i modelli di previsione o di serie temporali. .  
  
### <a name="requirements"></a>Requisiti  
 Per creare una struttura di data mining, è necessario disporre di una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È necessaria una connessione anche se si utilizzano strutture temporanee. Per ulteriori informazioni su come creare o modificare una connessione, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
