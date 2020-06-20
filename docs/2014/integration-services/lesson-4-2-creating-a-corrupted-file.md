---
title: 'Passaggio 2: Creazione di un file danneggiato | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f793f2cadf46d4a5431c01f5a1b1966ffad6fd55
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968201"
---
# <a name="step-2-creating-a-corrupted-file"></a>Passaggio 2: Creazione di un file danneggiato
  Per illustrare la configurazione e la gestione degli errori di trasformazione, è necessario creare un file flat di esempio che nel corso dell'elaborazione generi l'errore di un componente.  
  
 In questa attività verrà creata una copia di un file flat di esempio esistente. L'utente aprirà quindi il file in Blocco note e modificherà la colonna **CurrencyID** per assicurarsi che non si produca una corrispondenza durante la ricerca di trasformazioni. Quando il nuovo file verrà elaborato, l'esito negativo della ricerca impedirà l'esecuzione della trasformazione Currency Key Lookup e quindi del resto del pacchetto. Dopo aver creato il file di esempio danneggiato, verrà eseguito il pacchetto per osservare l'errore.  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>Per creare un file flat di esempio danneggiato  
  
1.  Aprire il file Currency_VEB.txt in Blocco note o in un altro editor di testo.  
  
     I dati di esempio sono inclusi nei pacchetti di lezioni di SSIS. Per scaricare i dati di esempio e i pacchetti di lezioni, effettuare le operazioni seguenti.  
  
    1.  Passare a [Integration Services Product Samples](https://go.microsoft.com/fwlink/?LinkID=267527).  
  
    2.  Fare clic sulla scheda **Downloads** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
2.  Utilizzare la funzionalità Trova e Sostituisci dell'editor di testo per trovare tutte le istanze di `VEB` e sostituirle con `BAD` .  
  
3.  Nella stessa cartella degli altri file di dati di esempio, salvare il file modificato come `Currency_BAD.txt` .  
  
    > [!IMPORTANT]  
    >  Assicurarsi che `Currency_BAD.txt` venga salvato la stessa cartella degli altri file di dati di esempio.  
  
4.  Chiudere l'editor di testo.  
  
### <a name="to-verify-that-an-error-will-occur-during-run-time"></a>Per accertarsi che in fase di runtime si verifichi un errore  
  
1.  Scegliere **Avvia debug**dal menu **debug** .  
  
     Alla terza iterazione del flusso di dati, la trasformazione Lookup Currency Key tenta di elaborare il file Currency_BAD.txt e ha esito negativo. L'errore della trasformazione provoca l'errore dell'intero pacchetto.  
  
2.  Scegliere **Arresta debug** dal menu **Debug**.  
  
3.  Nell'area di progettazione fare clic sulla scheda **Risultati esecuzione** .  
  
4.  Esplorare il registro e verificare che sia stato generato l'errore non gestito seguente:  
  
     `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    >  Il numero 27 è l'ID del componente. Questo valore viene assegnato quando si compila il flusso di dati e può essere diverso da quello nel pacchetto.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Passaggio 3: Aggiunta del reindirizzamento del flusso degli errori](lesson-4-3-adding-error-flow-redirection.md)  
  
  
