---
title: 'Attività 7: aggiunta della trasformazione pulizia DQS al flusso di dati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 209659609c2cf19196cc35050fb32e39e079d1c7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65488948"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Attività 7: Aggiunta della trasformazione DQS Cleansing al flusso di dati
  In questa attività viene aggiunta una trasformazione DQS Cleansing al flusso di dati per pulire i dati di input del fornitore tramite DQS. Per ulteriori informazioni sulla trasformazione, vedere **[trasformazione della pulizia DQS](https://msdn.microsoft.com/library/ee677619.aspx)** .  
  
1.  Fare clic con il pulsante destro del mouse su **DQS cleaning** nella scheda **flusso di dati** e scegliere **Rinomina**. Digitare **cleane Supplier Data**e premere **invio**.  
  
2.  Selezionare **Leggi dati fornitore dal file di Excel**. Trascinare il connettore blu per **pulire i dati fornitore**. I componenti sono ora collegati.  
  
     ![Leggere dati fornitore-> pulire i dati fornitore](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "Leggi dati fornitore -> Pulisci dati fornitore")  
  
3.  Fare doppio clic su **Pulisci dati fornitore**.  
  
4.  **Nell'Editor trasformazione DQS**, fare clic su **nuovo** accanto all' **elenco a discesa Gestione connessione Data Quality**.  
  
5.  Nella finestra di dialogo **gestione connessione DQS** , digitare **(local)** o **punto** (.) per connettersi al server locale. In questa lezione si presuppone che in un server locale sia installato DQS.  
  
6.  Fare clic su **Test connessione** per testare la connessione al server DQS.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
8.  Selezionare **Suppliers** per **Data Quality Knowledge base**.  
  
     ![Editor trasformazione DQS Cleansing - KB fornitori](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Editor trasformazione DQS Cleansing - KB fornitori")  
  
9. Passare alla scheda **mapping** nella parte superiore.  
  
10. **Nelle colonne di input disponibili**selezionare **Supplier Name**, **ContactEmailAddress**, **address line**, **City**, **state**, **Country**e **zip code** selezionando le caselle di controllo.  
  
     ![Editor trasformazione DQS Cleansing - Mapping](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor trasformazione DQS Cleansing - Mapping")  
  
11. Nel riquadro inferiore eseguire il mapping di queste colonne usando gli elenchi a discesa nella colonna **dominio** :  
  
    |Colonna|Dominio|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Indirizzo di posta elettronica del contatto|  
    |Riga indirizzo|Riga indirizzo|  
    |city|city|  
    |State|State|  
    |Country|Country|  
    |Zip Code|Zip|  
  
12. Fare clic su **OK** per chiudere la finestra di dialogo **Editor trasformazione di pulizia DQS** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 8: Aggiunta della trasformazione Suddivisione condizionale all'output di pulizia della suddivisione](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
