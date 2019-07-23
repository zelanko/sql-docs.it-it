---
title: 'Passaggio 3: Testare il pacchetto della lezione 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b7cfc1a4c6856debd52097b89587167060d212c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082198"
---
# <a name="lesson-6-3-test-the-lesson-6-package"></a>Lezione 6-3: Testare il pacchetto della lezione 6

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


In fase di esecuzione il pacchetto ottiene il valore per la proprietà **Directory** dal parametro **VarFolderName**.  
  
Per verificare che il pacchetto aggiorni la proprietà **Directory**, eseguire il pacchetto. Poiché sono stati copiati tre file di dati di esempio nella nuova directory, il flusso di dati viene eseguito tre volte.
  
## <a name="check-the-package-layout"></a>Verificare il layout del pacchetto  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 6 siano simili agli oggetti visualizzati nelle figure seguenti:   
  
**Flusso di controllo**  
  
![Flusso di controllo](../integration-services/media/task4lesson2control.gif "Flusso di controllo")  
  
**Flusso di dati**  
  
![Flusso di dati](../integration-services/media/task5lesson5data.gif "Flusso di dati")  
  
## <a name="test-the-lesson-6-package"></a>Testare il pacchetto della lezione 6  
  
1.  Selezionare **Avvia debug** dal menu **Debug**.  
  
2.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 4: Distribuire il pacchetto della lezione 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
