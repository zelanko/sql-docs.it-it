---
title: 'Attività 15: compilazione ed esecuzione del progetto SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822989"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Attività 15: Compilazione ed esecuzione del progetto SSIS

  In questa attività viene compilato ed eseguito il progetto SSIS. Se nel computer è installata la versione a 64 bit di Excel 2010, è necessario impostare il valore di **Run64BitRuntime** su **false** per il funzionamento dell'origine Excel.  
  
1.  Nella finestra di **Esplora soluzioni** fare clic su **progetto** nel menu e quindi su **Proprietà CleanseAndCurateSuppliers**.  
  
2.  Nella finestra di dialogo **Proprietà** espandere **proprietà di configurazione** a sinistra e fare clic su **debug**.  
  
3.  Impostare **Run64BitRuntime** su **false**.  
  
     ![Proprietà progetto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "Proprietà progetto CleanseAndCurateSuppliers")  
  
4.  Scegliere **OK** per chiudere la finestra di dialogo **Proprietà**.  
  
5.  Fare clic su **Compila** sulla barra dei menu e quindi su **Compila CleanseAndCurateSuppliers**. Assicurarsi che non siano presenti errori di compilazione.  
  
6.  Fare clic su **debug** nella barra dei menu e fare clic su **Avvia debug**.  
  
7.  Esaminare i messaggi nella finestra di stato e verificare che il pacchetto sia **stato** eseguito e terminato correttamente.  
  
     ![Risultati dalla finestra di stato](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "Risultati dalla finestra di stato")  
  
     ![Stato finale dalla finestra di stato](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "Stato finale dalla finestra di stato")  
  
8.  Fare clic su **debug** nella barra dei menu e fare clic su **Interrompi debug** per arrestare la sessione di debug. Se il pacchetto ha esito negativo, è necessario abilitare i visualizzatori dati e verificare il flusso dei dati tra i componenti.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 16: Verifica con Gestione dati master](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
