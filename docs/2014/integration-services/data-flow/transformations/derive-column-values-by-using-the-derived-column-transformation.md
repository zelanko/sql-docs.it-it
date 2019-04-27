---
title: Derivare i valori di colonna tramite la trasformazione Colonna derivata | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- columns [Integration Services]
- derived columns
- columns [Integration Services], values
- Derived Column transformation
ms.assetid: 28b07746-fc6f-42b2-b741-9de6fac3f29c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 39b8e065b6b3cbd013089700de07376edc9a656c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770688"
---
# <a name="derive-column-values-by-using-the-derived-column-transformation"></a>Derivazione di valori di colonna tramite la trasformazione Colonna derivata
  È possibile aggiungere e configurare una trasformazione Colonna derivata solo se il pacchetto include già almeno un'attività Flusso di dati e un'origine.  
  
 Nella trasformazione Colonna derivata vengono utilizzate espressioni per aggiornare i valori di colonne esistenti o aggiungere valori a nuove colonne. Quando si sceglie di aggiungere valori a nuove colonne, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene valutata l'espressione e vengono definiti di conseguenza i metadati delle colonne. Se ad esempio un'espressione determina la concatenazione di due colonne, ognuna con tipo di dati DT_WSTR e lunghezza di 50, con uno spazio tra i valori delle due colonne, la nuova colonna dispone del tipo di dati DT_WSTR e di una lunghezza di 101. È possibile aggiornare il tipo di dati di nuove colonne. L'unico requisito è rappresentato dal fatto che il tipo di dati deve essere compatibile con i dati inseriti. Nella finestra di dialogo **Editor trasformazione Colonna derivata** viene ad esempio generato un errore di convalida quando si assegna un valore di data a una colonna con tipo di dati integer. A seconda del tipo di dati selezionato, è possibile specificare la lunghezza, la precisione, la scala e la tabella codici della colonna.  
  
### <a name="to-derive-column-values"></a>Per derivare valori di colonna  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**, trascinare la trasformazione Colonna derivata sull'area di progettazione.  
  
4.  Connettere la trasformazione Colonna derivata al flusso di dati trascinando il connettore dall'origine o dalla trasformazione precedente alla trasformazione Colonna derivata.  
  
5.  Fare doppio clic sulla trasformazione Colonna derivata.  
  
6.  Nella finestra di dialogo **Editor trasformazione Colonna derivata** compilare le espressioni da usare come condizioni trascinando variabili, colonne, funzioni e operatori nella colonna **Espressione** della griglia. In alternativa, digitare l'espressione nella colonna **Espressione** .  
  
    > [!NOTE]  
    >  Se l'espressione non è valida, il testo dell'espressione viene evidenziato e tramite una descrizione comando nella colonna vengono descritti gli errori.  
  
7.  Nell'elenco **Colonna derivata** selezionare **\<aggiungi come nuova colonna>** per scrivere il risultato della valutazione dell'espressione in una nuova colonna oppure selezionare una colonna esistente per aggiornarla con il risultato della valutazione.  
  
     Se si è scelto di usare una nuova colonna, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene valutata l'espressione e viene assegnato un tipo di dati alla colonna, a seconda del tipo di dati, della lunghezza, della precisione, della scala e della tabella codici.  
  
8.  Se si usa una nuova colonna, selezionare un tipo di dati nell'elenco **Tipo di dati** . A seconda del tipo di dati selezionato, aggiornare facoltativamente i valori nelle colonne **Lunghezza**, **Precisione**, **Scala**e **Tabella codici** . I metadati delle colonne esistenti non possono essere modificati.  
  
9. Facoltativamente, modificare i valori nella colonna **Nome colonna derivata** .  
  
10. Per configurare l'output degli errori, fare clic su **Configura output errori**. Per altre informazioni, vedere [Configurare un output degli errori in un componente del flusso di dati](../../configure-an-error-output-in-a-data-flow-component.md).  
  
11. Fare clic su **OK**.  
  
12. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Derived Column Transformation](derived-column-transformation.md)   
 [Tipi di dati di Integration Services](../integration-services-data-types.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)   
 [Percorsi in Integration Services](../integration-services-paths.md)   
 [Attività Flusso di dati](../../control-flow/data-flow-task.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md)  
  
  
