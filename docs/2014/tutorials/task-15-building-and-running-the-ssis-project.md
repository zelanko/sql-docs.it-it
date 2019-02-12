---
title: "Attività 15: Compilazione e l'esecuzione del progetto SSIS | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.openlocfilehash: 1dc31f9b3df500e862236d4125fb1de99bc93eda
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022806"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Attività 15: Compilazione ed esecuzione del progetto SSIS
  In questa attività viene compilato ed eseguito il progetto SSIS. Se si dispone della versione a 64 bit di Excel 2010 installato nel computer, è necessario impostare il valore di **Run64BitRuntime** al **False** per l'origine Excel da utilizzare.  
  
1.  Nel **Esplora soluzioni** finestra, fare clic su **Project** dal menu, fare clic su **proprietà CleanseAndCurateSuppliers**.  
  
2.  Nel **delle proprietà** finestra di dialogo espandere **le proprietà di configurazione** a sinistra e fare clic su **debug**.  
  
3.  Impostare **Run64BitRuntime** al **False**.  
  
     ![Proprietà progetto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "proprietà progetto CleanseAndCurateSuppliers")  
  
4.  Fare clic su **OK** per chiudere la **proprietà** nella finestra di dialogo.  
  
5.  Fare clic su **compilare** sulla barra dei menu e quindi su **compila CleanseAndCurateSuppliers**. Assicurarsi che non siano presenti errori di compilazione.  
  
6.  Fare clic su **Debug** nella barra dei menu e fare clic su **Avvia debug**.  
  
7.  Esaminare i messaggi nella **lo stato di avanzamento** finestra e verificare che il pacchetto eseguito e completato correttamente.  
  
     ![Finestra di stato è dovuta](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "risultante dalla finestra di stato")  
  
     ![Lo stato finale dalla finestra di stato](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "lo stato finale dalla finestra di stato")  
  
8.  Fare clic su **Debug** sulla barra dei menu e quindi su **arresta debug** per arrestare la sessione di debug. Se il pacchetto ha esito negativo, è necessario abilitare i visualizzatori dati e verificare il flusso dei dati tra i componenti.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 16: Verifica con gestione dati Master](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
