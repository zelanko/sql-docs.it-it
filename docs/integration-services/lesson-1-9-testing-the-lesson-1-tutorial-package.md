---
description: "Passaggio 9: Testare il pacchetto creato nella lezione 1 dell'esercitazione"
title: "Passaggio 9: Testare il pacchetto creato nella lezione 1 dell'esercitazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 758f5e0c312afc2a8310743f917cc00a1c43462c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462013"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>Lezione 1-9: Testare il pacchetto della lezione 1

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



In questa esercitazione verranno effettuate le attività seguenti:  
  
-   Creazione di un nuovo progetto [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Configurazione delle gestioni connessioni necessarie al pacchetto per connettersi ai dati di origine e di destinazione.  
  
-   Aggiunta di un flusso di dati che preleva i dati da un'origine file flat, esegue le necessarie trasformazioni Ricerca sui dati e configura i dati per la destinazione.  
  
Il pacchetto è ora completo e pronto per essere testato.
  
## <a name="check-the-package-components"></a>Controllare i componenti del pacchetto
  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 1 contengano gli oggetti visualizzati nelle figure seguenti.  
  
**Flusso di controllo** 
  
![Flusso di controllo nel pacchetto](../integration-services/media/task9lesson1control.gif "Flusso di controllo nel pacchetto")  
  
**Flusso di dati**  
  
![Flusso di dati nel pacchetto](../integration-services/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
## <a name="run-the-lesson-1-package"></a>Eseguire il pacchetto della lezione 1  
  
1.  Scegliere **Avvia debug** dal menu **Debug**.  
  
    Il pacchetto viene eseguito e vengono aggiunte 1.097 righe alla tabella dei fatti **NewFactCurrencyRate** in **AdventureWorksDW2012**. Per verificare questo risultato, selezionare la scheda **Flusso di dati**.
  
2.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="go-to-next-lesson"></a>Passare alla lezione successiva
[Lezione 2: Aggiungere cicli con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di progetti e pacchetti](packages/run-integration-services-ssis-packages.md) 
  
  
  
