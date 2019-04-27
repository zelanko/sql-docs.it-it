---
title: Modificare le etichette (componenti aggiuntivi Data Mining SQL Server dati) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74e2322416ec06c36a7834f35581ed611480b6e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748324"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>Modifica etichette (componenti aggiuntivi Data mining di SQL Server)
  ![Icona di Office 13 per lo strumento Modifica etichette](media/dm13-relabel.gif "sull'icona di Office 13 per lo strumento Modifica etichette dati")  
  
 Il client di data mining per Excel consente di creare nuove etichette per i dati per semplificare la comprensione dei risultati dell'analisi.  
  
 I motivi di modifica delle etichette includono:  
  
-   I dati includono i risultati che sono stati codificati, ad esempio 1 per maschio e 2 per femmina.  
  
-   Sono valori numerici di bucket e si desidera fornire agli intervalli un nome descrittivo.  
  
-   Si desidera semplificare i nomi lunghi.  
  
## <a name="using-the-relabel-wizard"></a>Utilizzo della procedura guidata Modifica etichette  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **Pulisci** e quindi selezionare **Rietichettare**.  
  
2.  Selezionare la tabella o l'intervallo di dati contenente i dati che si desidera correggere.  
  
3.  Nel **rietichettare** pagina della procedura guidata, selezionare una singola colonna scegliendo la colonna nell'elenco a discesa o facendo clic nella colonna il **esempi di dati** riquadro.  
  
     Il **esempi di dati** riquadro Mostra solo circa 50 righe di dati, ma vengono campionate per garantire di vedere un'ampia gamma di valori.  
  
     Fare clic sull'intestazione di colonna per **conteggio** per ordinare per il conteggio di ogni valore.  
  
     È possibile anche ordinare **etichette originali**, che è utile se si desidera modificare prima le etichette tutti i valori massimi o minimi.  
  
4.  Nel **rietichettare** pagina di dati della procedura guidata, rivedere i valori nel **etichette originali** colonna e decidere come si desidera raggrupparli o modificarli.  
  
5.  Digitare un nuovo valore nella riga in **nuove etichette**. È inoltre possibile scegliere un valore nell'elenco dei valori esistenti. Mentre si digitano, i nuovi valori diventano disponibili per essere subito riutilizzati.  
  
6.  Dopo l'immissione di numero di righe sufficiente, fare clic su **successivo**e il **Seleziona destinazione** pagina, scegliere in cui si salveranno i dati stati.  
  
    -   **Aggiungi come nuova colonna al foglio di lavoro corrente**  
  
         Fare clic per aggiungere una nuova colonna alla tabella contenente i nuovi valori.  
  
    -   **Copiare i dati del foglio modificati in un nuovo foglio di lavoro**  
  
         Fare clic per creare un nuovo foglio di lavoro contenente i dati aggiornati.  
  
    -   **Modificare i dati sul posto**  
  
         Fare clic per sostituire i dati originali con i nuovi valori.  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione e pulizia dei dati](exploring-and-cleaning-data.md)  
  
  
