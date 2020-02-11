---
title: "Passaggio 5: Aggiunta e configurazione dell'origine file flat | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32b95a5d156ae52394b7128b024c86b9a7e308b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62891539"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>Passaggio 5: Aggiunta e configurazione dell'origine file flat
  In questa attività verrà aggiunta e configurata l'origine file flat al pacchetto. Un'origine file flat è un componente del flusso di dati che utilizza i metadati definiti dalla gestione connessione file flat per specificare il formato e la struttura dei dati da estrarre dal file flat tramite un processo di trasformazione. È possibile configurare l'origine file flat per estrarre dati da un singolo file flat utilizzando la definizione del formato del file specificata dalla gestione connessione file flat.  
  
 Per questa esercitazione verrà configurata l'origine file flat per l'utilizzo `Sample Flat File Source Data` della gestione connessione creata in precedenza.  
  
### <a name="to-add-a-flat-file-source-component"></a>Per aggiungere un componente origine file flat  
  
1.  Aprire la finestra di progettazione **flusso di dati** facendo doppio clic sull' `Extract Sample Currency Data` attività flusso di dati o facendo clic sulla **scheda flusso di dati**.  
  
2.  Nella **Casella degli strumenti SSIS**espandere **OtherSources**, quindi trascinare un' **Origine file flat** sull'area di progettazione della scheda **Flusso di dati** .  
  
3.  Nell'area di progettazione **flusso di dati** fare clic con il pulsante destro del mouse sull' **origine file flat**appena aggiunta, scegliere **Rinomina**e `Extract Sample Currency Data`modificare il nome in.  
  
4.  Fare doppio clic sull'origine file flat per aprire la finestra di dialogo Editor origine file flat.  
  
5.  Nella casella **gestione connessione file flat** selezionare `Sample Flat File Source Data`.  
  
6.  Fare clic su **Colonne** e verificare che i nomi delle colonne siano corretti.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic con il pulsante destro del mouse sull'origine file flat e scegliere **Proprietà**.  
  
9. Nella Finestra Proprietà verificare che la `LocaleID` proprietà sia impostata su **inglese (Stati Uniti)**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 6: Aggiunta e configurazione delle trasformazioni Ricerca](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Origine file flat](data-flow/flat-file-source.md)   
 [Editor gestione connessione file flat &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)  
  
  
