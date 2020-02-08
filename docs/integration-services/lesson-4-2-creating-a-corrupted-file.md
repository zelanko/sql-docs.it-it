---
title: 'Passaggio 2: Creare un file danneggiato | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd9266512675c4127a99903e6de0d1da5ccaec70
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295954"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>Lezione 4-2: Creare un file danneggiato

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Per illustrare la configurazione e la gestione degli errori di trasformazione, è necessario creare un file flat di esempio che nel corso dell'elaborazione generi l'errore di un componente.  
  
In questa attività viene creata una copia di un file flat di esempio esistente. Aprire quindi il file nel Blocco note e modificare la colonna **CurrencyID** in modo che contenga un valore errato, che genera un errore di ricerca. Quando il file danneggiato viene elaborato, l'esito negativo della ricerca impedisce l'esecuzione della trasformazione Currency Key Lookup e quindi del resto del pacchetto. Dopo aver creato il file di esempio danneggiato, viene eseguito il pacchetto per osservare l'errore.  
  
## <a name="create-a-corrupted-sample-flat-file"></a>Creare un file flat di esempio danneggiato  
  
1.  Aprire il file **Currency_VEB.txt** in Blocco note o in un altro editor di testo.  
  
2.  Usare la funzionalità di ricerca e sostituzione dell'editor di testo per trovare tutte le istanze di **VEB** e sostituirle con **BAD**.  
  
3.  Nella stessa cartella degli altri file di dati di esempio, salvare il file modificato con il nome **Currency_BAD.txt**.  
  
    > [!NOTE]  
    > Assicurarsi che il file **Currency_BAD.txt** venga salvato nella stessa cartella degli altri file di dati di esempio.  
  
4.  Chiudere l'editor di testo.  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>Accertarsi che in fase di runtime si verifichi un errore  
  
1.  Selezionare **Avvia debug** dal menu **Debug**.  
  
    Alla terza iterazione del flusso di dati, la trasformazione Lookup Currency Key tenta di elaborare il file **Currency_BAD.txt** e ha esito negativo. L'errore della trasformazione provoca l'errore dell'intero pacchetto.  
  
2.  Selezionare **Arresta debug** dal menu **Debug**.  
  
3.  Nell'area di progettazione, selezionare la scheda **Risultati esecuzione**.  
  
4.  Esplorare il registro e verificare che sia stato generato l'errore non gestito seguente:  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > Il numero 27 è l'ID del componente. Questo valore viene assegnato quando si compila il flusso di dati e può essere diverso da quello nel pacchetto.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo  
[Passaggio 3: Aggiungere il reindirizzamento del flusso degli errori](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
