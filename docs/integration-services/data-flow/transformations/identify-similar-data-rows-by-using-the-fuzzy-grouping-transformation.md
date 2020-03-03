---
title: Identificare righe di dati simili con la trasformazione Raggruppamento fuzzy | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8acc9dfcfc908a0e1c196eb7b9ac2c6af088eaf
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903919"
---
# <a name="identify-similar-data-rows-with-the-fuzzy-grouping-transformation"></a>Identificare righe di dati simili con la trasformazione Raggruppamento fuzzy

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile aggiungere e configurare una trasformazione Raggruppamento fuzzy solo se il pacchetto include già almeno un'attività Flusso di dati e un'origine.  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>Per implementare una trasformazione Raggruppamento fuzzy in un flusso di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** , quindi da **Casella degli strumenti**trascinare la trasformazione Raggruppamento fuzzy sull'area di progettazione.  
  
4.  Connettere la trasformazione Raggruppamento fuzzy al flusso di dati trascinando il connettore dall'origine dati o da una trasformazione precedente alla trasformazione Raggruppamento fuzzy.  
  
5.  Fare doppio clic sulla trasformazione Raggruppamento fuzzy.  
  
6.  Nella scheda **Gestione connessione** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** selezionare una gestione connessione OLE DB che consenta la connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  La trasformazione richiede una connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per creare tabelle e indici temporanei.  
  
7.  Fare clic sulla scheda **Colonne** e, nell'elenco **Colonne di input disponibili** , selezionare la casella di controllo corrispondente alla colonna di input da usare per identificare righe simili nel set di dati.  
  
8.  Per identificare le colonne di input da passare direttamente all'output della trasformazione, selezionare le caselle di controllo nella colonna **Pass-through** . Le colonne pass-through non vengono coinvolte nel processo di identificazione delle righe duplicate.  
  
    > [!NOTE]  
    >  Le colonne di input utilizzate per il raggruppamento vengono automaticamente selezionate come colonne pass-through e non possono essere deselezionate mentre sono in uso per il raggruppamento.  
  
9. Facoltativamente, aggiornare i nomi delle colonne di output nella colonna **Alias di output** .  
  
10. Facoltativamente, aggiornare i nomi delle colonne elaborate nella colonna **Alias di output gruppo** .  
  
    > [!NOTE]  
    >  I nomi predefiniti delle colonne vengono ottenuti aggiungendo il suffisso "_clean" ai nomi delle colonne di input.  
  
11. Facoltativamente, digitare nella colonna **Tipo di corrispondenza** il tipo di corrispondenza da utilizzare.  
  
    > [!NOTE]  
    >  È necessario utilizzare la corrispondenza fuzzy almeno per una colonna.  
  
12. Specificare le colonne con livello di somiglianza minimo nella colonna **Somiglianza minima** . Il valore deve essere compreso tra 0 e 1. Più il valore è vicino a 1, più i valori nelle colonne di input dovranno essere simili per formare un gruppo. Una somiglianza minima pari a 1 indica una corrispondenza esatta.  
  
13. Facoltativamente, aggiornare i nomi delle colonne con somiglianza nella colonna **Alias di output somiglianza** .  
  
14. Per specificare la modalità di gestione dei numeri nei valori dei dati, aggiornare i valori nella colonna **Numerali** .  
  
15. Per specificare la modalità con cui la trasformazione deve confrontare i dati stringa contenuti in una colonna, modificare la selezione predefinita delle opzioni di confronto nella colonna **Flag di confronto** .  
  
16. Fare clic sulla scheda **Avanzate** per modificare i nomi delle colonne che la trasformazione aggiunge all'output per l'identificatore di riga univoco (_key_in), l'identificatore di riga duplicato (_key_out) e il valore di somiglianza (_score).  
  
17. Facoltativamente, regolare la soglia di somiglianza spostando il dispositivo di scorrimento.  
  
18. Facoltativamente, deselezionare le caselle di controllo in Delimitatori token per ignorare i delimitatori presenti nei dati.  
  
19. Fare clic su **OK**.  
  
20. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Attività Flusso di dati](../../../integration-services/control-flow/data-flow-task.md)  
  
  
