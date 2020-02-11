---
title: Pianificare i criteri | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8becd7ad30acf1ea2a63feae4760091aede70c06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033503"
---
# <a name="schedule-the-policies"></a>Pianificazione criteri
  In questa attività verrà eseguita la pianificazione dei criteri per procedure consigliate importati nell'attività precedente.  
  
### <a name="to-schedule-the-best-practices-policies"></a>Per pianificare i criteri per procedure consigliate  
  
1.  In Esplora oggetti espandere **gestione**, **Gestione criteri**e **criteri, fare**clic con il pulsante destro del mouse su criteri per procedure consigliate e quindi scegliere **Proprietà**.  
  
    > [!NOTE]  
    >  In alternativa, per individuare facilmente i criteri associati alle procedure consigliate e per ordinare le categorie procedure consigliate, espandere **gestione**, **Gestione criteri**, quindi fare clic su **criteri**. Scegliere **Dettagli Esplora oggetti** dal menu **Visualizza**. Nel riquadro **dettagli Esplora oggetti** fare clic sull'intestazione **categoria** per ordinare i criteri per categoria. I criteri per procedure consigliate prevedono il prefisso **Microsoft Best Practices**. Fare clic con il pulsante destro del mouse sui criteri che si desidera configurare, quindi scegliere **Proprietà**.  
  
2.  Nella pagina **generale** della finestra di dialogo **Apri criteri** , nell'elenco **modalità di valutazione** , fare clic **su pianificazione**.  
  
3.  Accanto alla casella **pianificazione** fare clic su **Seleziona** per specificare una pianificazione esistente oppure fare clic su **nuova** per creare una nuova pianificazione.  
  
4.  Dopo aver configurato una pianificazione, è possibile selezionare la casella di controllo **abilitato** nella parte superiore della pagina per abilitare i criteri pianificati.  
  
5.  Ripetere i passaggi da 1 a 4 per tutti i criteri che si desidera pianificare.  
  
    > [!NOTE]  
    >  Per visualizzare i risultati di valutazione dopo l'esecuzione di criteri pianificati, aprire il log Cronologia criteri nell'istanza di destinazione. Per aprire il log, fare clic con il pulsante destro del mouse su **Gestione criteri**, quindi scegliere **Visualizza cronologia**.  
  
## <a name="summary"></a>Summary  
 I criteri pianificati sono stati configurati per essere eseguiti in un'istanza singola di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se si desidera distribuire i criteri pianificati in più istanze, continuare con la prossima attività in questa esercitazione.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Distribuzione di criteri pianificati in istanze multiple](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
