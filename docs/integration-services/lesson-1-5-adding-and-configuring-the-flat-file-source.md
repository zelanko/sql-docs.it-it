---
title: "Passaggio 5: Aggiungere e configurare l'origine file flat | Microsoft Docs"
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e95b86d2d29bb3883f6fd76db29f17e5936d1b53
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283682"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>Lezione 1-5: Aggiungere e configurare l'origine file flat

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


In questa attività verrà aggiunta al pacchetto e configurata un'origine file flat. Un'origine file flat è un componente flusso di dati che usa i metadati definiti da una gestione connessione file flat. Questi metadati specificano il formato e la struttura dei dati che devono essere estratti dal file flat da un processo di trasformazione. L'origine file flat estrae dati da un unico file flat usando le definizioni di formato di file presenti nella gestione connessione file flat.  
  
Per questa attività verrà configurata l'origine file flat in modo da usare la gestione connessione **Sample Flat File Source Data** creata in precedenza.  
  
## <a name="add-a-flat-file-source-component"></a>Aggiungere un componente origine file flat  
  
1.  Per aprire la finestra di progettazione **Flusso di dati** fare doppio clic sull'attività Flusso di dati **Extract Sample Currency Data** o selezionare la scheda **Flusso di dati**.  
  
2.  Nella **Casella degli strumenti SSIS**espandere **OtherSources**, quindi trascinare un' **Origine file flat** sull'area di progettazione della scheda **Flusso di dati** .  
  
3.  Nell'area di progettazione **Flusso di dati** fare clic con il pulsante destro del mouse sulla nuova **origine file flat**, selezionare **Rinomina**e cambiare il nome in **Extract Sample Currency Data**.  
  
4.  Fare doppio clic sull'origine file flat per aprire la finestra di dialogo **Editor origine file flat**.  
  
5.  Nel campo **Gestione connessione file flat** selezionare **Sample Flat File Source Data**.  
  
6.  Selezionare **Colonne** e verificare che i nomi delle colonne siano corretti.  
  
7.  Selezionare **OK**.  
  
8.  Fare clic con il pulsante destro del mouse sull'origine file flat e selezionare **Proprietà**.  
  
9. Nella finestra **Proprietà** verificare che la proprietà **LocaleID** sia impostata su **Inglese (Stati Uniti)** .  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 6: Aggiungere e configurare le trasformazioni Ricerca](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Vedere anche  
[Origine file flat](../integration-services/data-flow/flat-file-source.md)  
[Gestione connessione file flat](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  
