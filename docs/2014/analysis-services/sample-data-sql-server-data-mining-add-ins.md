---
title: Campionare i dati (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a69b2286abbc1ba4289fd482b1bbf5a2dfb3e7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070041"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>Dati di esempio (componenti aggiuntivi Data mining di SQL Server)
  ![Creazione guidata dei dati di partizione nella barra multifunzione Data Mining](media/dmc-partition.gif "Creazione guidata partizione dati sulla barra multifunzione Data Mining")  
  
 Il **dati di esempio** guidata rende più semplice dividere i dati di origine in due set, uno per la compilazione (training) del modello e uno per il modello di test. Questa procedura guidata consente inoltre di ricampionare i dati per compilare un nuovo set di dati che rappresenti meglio la destinazione.  
  
 La creazione del tipo appropriato di dati per il training e il testing dei modelli costituisce una parte importante del data mining, ma senza gli strumenti appropriati può rivelarsi un'operazione noiosa. La procedura guidata esegue il campionamento stratificato per assicurare che i set di training e di testing siano ben equilibrati.  
  
## <a name="random-sampling-and-oversampling"></a>Campionamento casuale e sovracampionamento  
 . Il campionamento casuale è il metodo migliore per garantire che i dati usati per il testing di un modello rappresentino fedelmente i dati usati per creare il modello. È possibile campionare in modo casuale i dati archiviati in Excel o in un'origine dati esterna  
  
 Se si usa l'opzione di campionamento casuale, il **dati di esempio** guidata automaticamente Crea set di dati di training e di test e vengono inseriti in fogli di lavoro di Excel separate per riferimento futuro.  
  
 Se i dati sono archiviati in una cartella di lavoro di Excel e non un'origine dati esterna, è anche possibile usare *sovracampionamento*. Con questa opzione, si specifica un valore di destinazione che potrebbe essere scarso nei dati e si usano la procedura guidata per raccogliere un set bilanciato che includa il valore di destinazione. È possibile usare la procedura guidata in modo da ottenere una percentuale di destinazione o da creare un determinato numero di righe.  
  
 Se si usa l'opzione di sovracampionamento, il **dati di esempio** procedura guidata crea un nuovo foglio di lavoro che contiene i dati di esempio bilanciati.  
  
## <a name="using-the-sample-data-wizard"></a>Utilizzo della procedura guidata Dati di esempio  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>Per dividere i dati in set di training e set di testing  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **i dati di esempio**.  
  
2.  Nel **selezione dati di origine** , specificare se il **dati** che si desidera partizione si trova in un intervallo di Excel o una tabella o in un'origine dati esterna.  
  
3.  Nel **Seleziona tipo di campionamento** , specificare se si desidera creare training set e set di dati di test tramite campionamento casuale oppure creare un nuovo set di dati tramite sovracampionamento.  
  
    > [!NOTE]  
    >  Se si usano un'origine dati esterna, è disponibile solo l'opzione di campionamento casuale. Se si desidera usare il sovracampionamento con i dati esterni, è possibile importare i dati in una cartella di lavoro di Excel usando una connessione dati di Excel, quindi usare la procedura guidata Dati di esempio.  
  
4.  Impostare le opzioni specifiche per il metodo di campionamento selezionato.  
  
    -   Per il campionamento casuale, specificare una percentuale dei dati originali da usare per il testing oppure il numero totale di righe da usare nel set di dati di test.  
  
    -   Per il sovracampionamento, selezionare la colonna e il valore che si desidera evidenziare. Specificare quindi il numero totale di righe del nuovo set di dati e la percentuale di righe del nuovo set di dati che deve includere il valore di destinazione.  
  
         Il valore di destinazione per il sovracampionamento deve essere un valore discreto. Non è possibile sovracampionare dati numerici continui.  
  
5.  Nel **pagina Finish**, accettare i nomi predefiniti per i nuovi set di dati o digitare un nuovo nome.  
  
     Tramite la procedura guidata vengono creati nuovi fogli di lavoro per ogni set di dati.  
  
 La maggior parte delle procedure guidate nel Client di data mining per Excel consente di separare in modo casuale i dati in set di training e di testing. Se tuttavia si usano le procedure guidate, i dati rimangono nello stesso foglio di lavoro o in un'altra origine dati e le informazioni che indicano se una particolare riga è un case di testing o di training vengono archiviate internamente. Al contrario, quando si usa la **dati di esempio** procedura guidata, il test e i dati di training vengono inseriti in fogli di lavoro per semplificarne la consultazione al distinti.  
  
## <a name="related-options"></a>Opzioni correlate  
 Andando avanti con la procedura guidata, saranno disponibili queste opzioni:  
  
|Opzioni|Commenti|  
|-------------|--------------|  
|Finestra di dialogo Selezione dati di origine (Client di data mining per Excel)|Selezionare una tabella o un intervallo di Excel contenente i dati. Se si desidera usare dati esterni, i dati possono essere relazionali, ma devono essere inclusi in un'origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. T|  
|Pagina Selezione tipo di campionamento (client di data mining per Excel)|Se si usano un'origine dati esterna, è possibile usare solo l'opzione di campionamento casuale. Inoltre, è necessario specificare il numero di righe da creare nel set di dati finale, tramite il **conteggio righe** opzione. Non è possibile specificare una percentuale dei dati di origine.|  
|Pagina Campionamento casuale (client di data mining per Excel)|È possibile copiare una percentuale di righe dall'origine o un numero di righe specifico.|  
|Pagina Sovracampionamento (client di data mining per Excel)|**Stato di destinazione**<br /><br /> Selezionare nell'elenco un valore sottorappresentato nel set di dati originale. Tramite il sovracampionamento sarà possibile aumentare la proporzione di righe di dati che includono questo stato.<br /><br /> **Dimensioni del campione**<br /><br /> Selezionare il numero totale di righe da estrarre. Questo valore rappresenta la dimensione del set di dati finale.|  
  
## <a name="other-sampling-options"></a>Altre opzioni di campionamento  
 Se le opzioni per il campionamento disponibili in questa procedura guidata non soddisfano specifiche esigenze, è possibile usare la trasformazione di campionamento in SQL Server Integration Services (SSIS) per campionare le righe di più origini dati.  
  
 Per altre informazioni, vedere [trasformazione campionamento righe](../integration-services/data-flow/transformations/row-sampling-transformation.md) e [trasformazione campionamento percentuale](../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elenco di controllo per la preparazione di data mining](checklist-of-preparation-for-data-mining.md)  
  
  
