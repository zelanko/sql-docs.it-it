---
title: Impostare il tipo di dati di una colonna (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 34e2d508-7b64-4503-a4f0-c6c6ad5f8a44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82b2d4a687c490ed1909a27fc55fdece9cc3662c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794362"
---
# <a name="set-the-data-type-of-a-column-ssas-tabular"></a>Impostare il tipo di dati di una colonna (SSAS tabulare)
  Quando si importano o incollano dati in un modello, Progettazione modelli consentirà di rilevare e applicare automaticamente i tipi di dati. Dopo aver aggiunto i dati al modello, è possibile modificare manualmente il tipo di dati di una colonna per cambiarne la modalità di archiviazione oppure limitarsi a modificare il formato della modalità di visualizzazione dei dati.  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>Per modificare il tipo di dati o il formato di visualizzazione per una colonna  
  
1.  In Progettazione modelli selezionare la colonna per la quale si desidera modificare il tipo di dati o il formato di visualizzazione.  
  
2.  Nella finestra **Proprietà** della colonna effettuare uno dei passaggi seguenti:  
  
    -   Nella proprietà **Formato dati** selezionare un formato dati diverso.  
  
    -   Nella proprietà **Tipo di dati** selezionare un tipo di dati diverso.  
  
## <a name="considerations-when-changing-data-types"></a>Considerazioni in caso di modifica dei tipi di dati  
 Talvolta, quando si tenta di modificare il tipo di dati di una colonna o di selezionare una conversione dei dati, è possibile che si verifichi uno degli errori seguenti:  
  
-   Impossibile modificare il tipo di dati  
  
-   Impossibile modificare il tipo di dati della colonna  
  
 Tali errori potrebbero verificarsi anche se il tipo di dati è disponibile come opzione nell'elenco a discesa Tipo di dati. In questa sezione viene illustrata la causa di tali errori e viene mostrato come correggerli.  
  
### <a name="understanding-automatically-determined-data-types"></a>Informazioni sui tipi di dati determinati automaticamente  
 Quando si aggiungono dati a un modello, Progettazione modelli consente di controllare le colonne di dati per verificare quali tipi di dati sono contenuti in ogni colonna. Se i dati nella colonna in oggetto sono coerenti, alla colonna viene assegnato il tipo di dati più preciso.  
  
 Se invece si aggiungono dati da Excel o da un'altra origine che non impone l'utilizzo di un solo tipo di dati all'interno di ogni colonna, Progettazione modelli consentirà di assegnare un tipo di dati in grado di supportare tutti i valori nella colonna. Se pertanto in una colonna sono contenuti numeri di tipi diversi, ad esempio interi, numeri lunghi e valute, in Progettazione modelli verrà utilizzato un tipo di dati decimale. In alternativa, se in una colonna sono presenti numeri e testo, in Progettazione modelli verrà utilizzato il tipo di dati text. In Progettazione modelli non è disponibile un tipo di dati simile al tipo di dati generale disponibile in Excel.  
  
 Se pertanto in una colonna sono contenuti sia numeri sia valori di testo, non sarà possibile convertire la colonna in un tipo di dati numerico.  
  
 Nei modelli Business Intelligence Semantic Model sono disponibili i tipi di dati seguenti:  
  
|Tipi di dati dei modelli|  
|----------------------|  
|Text<br /><br /> Numero decimale<br /><br /> Numero intero<br /><br /> Currency<br /><br /> TRUE/FALSE<br /><br /> date|  
  
 Se il tipo di dati è errato o è diverso da quello desiderato, è possibile eseguire diverse operazioni:  
  
-   È possibile reimportare i dati. A tale scopo, aprire la connessione esistente all'origine dati e reimportare la colonna. A seconda del tipo di origine dati, è possibile applicare un filtro durante l'importazione per rimuovere i valori problematici.  
  
-   È possibile creare una formula DAX in una colonna calcolata per creare un nuovo valore del tipo di dati desiderato. La funzione TRUNC può ad esempio essere utilizzata per impostare un numero decimale su un Integer intero o è possibile combinare funzioni per l'elaborazione di informazioni e funzioni logiche per testare e convertire i valori.  
  
### <a name="understanding-data-conversion"></a>Informazioni sulla conversione dei dati  
 Se si verifica un errore quando si seleziona un'opzione di conversione dei dati, è possibile che il tipo di dati corrente della colonna non supporti la conversione selezionata. Non tutti i tipi di conversione sono consentiti per tutti i tipi di dati. È ad esempio possibile impostare una colonna su un tipo di dati Booleano solo se il tipo di dati corrente della colonna è un numero (intero o decimale) o è testo. È pertanto necessario scegliere un tipo di dati appropriato per i dati della colonna.  
  
 Dopo aver scelto un tipo di dati appropriato, l'utente riceverà una notifica relativa alle possibili modifiche ai dati, ad esempio perdita di precisione o troncamento, da Progettazione modelli. Fare clic su OK per accettare e modificare i dati con il nuovo tipo di dati.  
  
 Se il tipo di dati è supportato, ma tramite Progettazione modelli vengono individuati valori non supportati all'interno del nuovo tipo di dati, verrà visualizzato un altro errore e sarà necessario correggere i valori dei dati prima di procedere.  
  
 Per informazioni dettagliate sui tipi di dati usati nei modelli BI Semantic Model, sulla relativa modalità di conversione implicita e sull'impiego di tipi di dati diversi nelle formule, vedere [Data Types Supported &#40;SSAS Tabular&#41;](data-types-supported-ssas-tabular.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati supportati &#40;SSAS tabulare&#41;](data-types-supported-ssas-tabular.md)  
  
  
