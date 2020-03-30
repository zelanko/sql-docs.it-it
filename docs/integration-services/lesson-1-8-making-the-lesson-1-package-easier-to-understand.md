---
title: 'Passaggio 8: Annotare e formattare il pacchetto della lezione 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a67d7593ca63a2271fc94fc7203e9bb55d6efcc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71680972"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>Lezione 1-8: Annotare e formattare il pacchetto della lezione 1 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Dopo avere completato la configurazione del pacchetto della lezione 1, è il momento probabilmente di riordinarne il layout. Se le forme nei layout di controllo e del flusso di dati sono di dimensioni diverse o non sono disposte in modo uniforme, potrebbe essere più difficile comprendere il pacchetto.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Strumenti dati fornisce strumenti per formattare agevolmente il layout del pacchetto. Le caratteristiche di formattazione includono la possibilità di impostare forme di dimensioni uguali, di allineare le forme e di modificare la spaziatura orizzontale e verticale tra le forme.  
  
Un altro modo per rendere più comprensibili le funzionalità del pacchetto consiste nell'aggiunta di annotazioni descrittive.  
  
In questa attività verranno utilizzate le funzionalità di formattazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools per migliorare il layout del flusso di dati e aggiungere un'annotazione.  
  
## <a name="format-the-layout-of-the-data-flow"></a>Formattare il layout del flusso di dati  
  
1.  Se il pacchetto della lezione 1 non è aperto, fare doppio clic su **Lesson 1.dtsx** in **Esplora soluzioni**.  
  
2.  Selezionare la scheda **Flusso di dati**.  
  
3.  Per selezionare tutti i componenti del flusso di dati in una sola volta, usare **Modifica** > **Seleziona tutto**.
  
4.  Selezionare **Rendi uguali** dal menu **Formato**e quindi selezionare **Entrambe**.  
  
5.  Con gli oggetti del flusso di dati selezionati, selezionare **Allinea** dal menu **Formato**e quindi fare clic su **Al centro**.  

6.  Con gli oggetti del flusso di dati selezionati, scegliere **Spaziatura verticale** dal menu **Formato**, quindi selezionare **Rendi uguali**.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>Aggiungere un'annotazione al flusso di dati  
  
1.  Fare clic con il pulsante destro del mouse in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di dati e quindi selezionare **Aggiungi annotazione**.  
  
2.  Immettere o incollare il testo seguente nella casella delle annotazioni.  
  
        The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.
  
    Per eseguire il wrapping del testo nella casella delle annotazioni, inserire il cursore nel punto in cui si desidera iniziare una nuova riga e premere **INVIO**.  
  
    Se non si inserisce alcun testo nella casella delle annotazioni, quest'ultima scomparirà quando si farà clic al suo esterno.  A causa di questo comportamento, se si vuole incollare il testo nella casella di annotazione, copiare il testo negli Appunti prima di selezionare Aggiungi annotazione. 
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 9: Testare il pacchetto della lezione 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
