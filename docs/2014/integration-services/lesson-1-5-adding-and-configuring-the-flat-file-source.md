---
title: "Passaggio 5: Aggiunta e configurazione dell'origine file flat | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f1f50c3aed4429a3ba05a23a969d050c45778c34
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435848"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>Passaggio 5: Aggiunta e configurazione dell'origine file flat
  In questa attività verrà aggiunta e configurata l'origine file flat al pacchetto. Un'origine file flat è un componente del flusso di dati che utilizza i metadati definiti dalla gestione connessione file flat per specificare il formato e la struttura dei dati da estrarre dal file flat tramite un processo di trasformazione. È possibile configurare l'origine file flat per estrarre dati da un singolo file flat utilizzando la definizione del formato del file specificata dalla gestione connessione file flat.  
  
 Per questa esercitazione verrà configurata l'origine file flat per l'utilizzo della `Sample Flat File Source Data` gestione connessione creata in precedenza.  
  
### <a name="to-add-a-flat-file-source-component"></a>Per aggiungere un componente origine file flat  
  
1.  Aprire la finestra di progettazione **flusso di dati** facendo doppio clic sull' `Extract Sample Currency Data` attività flusso di dati o facendo clic sulla **scheda flusso di dati**.  
  
2.  Nella **Casella degli strumenti SSIS**espandere **OtherSources**, quindi trascinare un' **Origine file flat** sull'area di progettazione della scheda **Flusso di dati** .  
  
3.  Nell'area di progettazione **flusso di dati** fare clic con il pulsante destro del mouse sull' **origine file flat**appena aggiunta, scegliere **Rinomina**e modificare il nome in `Extract Sample Currency Data` .  
  
4.  Fare doppio clic sull'origine file flat per aprire la finestra di dialogo Editor origine file flat.  
  
5.  Nella casella **gestione connessione file flat** selezionare `Sample Flat File Source Data` .  
  
6.  Fare clic su **Colonne** e verificare che i nomi delle colonne siano corretti.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic con il pulsante destro del mouse sull'origine file flat e scegliere **Proprietà**.  
  
9. Nella Finestra Proprietà verificare che la `LocaleID` proprietà sia impostata su **inglese (Stati Uniti)**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 6: Aggiunta e configurazione delle trasformazioni Ricerca](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Origine file flat](data-flow/flat-file-source.md)   
 [Editor gestione connessione file flat &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)  
  
  
