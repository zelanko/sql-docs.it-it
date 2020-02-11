---
title: Sistema di risoluzione dei conflitti di replica interattivo Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.interactiveresolver.f1
ms.assetid: d3d4a480-782b-4b1d-b839-565c8cf6cb24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68ddc4f6b42dcc53445b8afaae0bc15e666a5711
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667283"
---
# <a name="microsoft-replication-interactive-conflict-resolver"></a>Sistema di risoluzione dei conflitti di replica interattivo Microsoft
  Il sistema di risoluzione dei conflitti interattivo può essere utilizzato per le sottoscrizioni di tipo merge sincronizzate tramite Gestione sincronizzazione Microsoft Windows e consente di visualizzare, confrontare, modificare e selezionare i risultati dei conflitti di dati. È inoltre disponibile il Visualizzatore conflitti, che consente di visualizzare e modificare i risultati dei conflitti dopo il commit. Con il sistema di risoluzione dei conflitti interattivo è possibile selezionare il risultato durante la sincronizzazione.  
  
> [!NOTE]  
>  I conflitti a livello di record logici non vengono visualizzati nel sistema di risoluzione interattivo. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opzioni  
 **Nome colonna**  
 Nome di tutte le colonne nella tabella. È possibile che una o più colonne contengano dati in conflitto. Indipendentemente da quali siano le colonne in conflitto, l'intera riga confermata sovrascriverà l'intera riga non confermata.  
  
 **Risoluzione suggerita**  
 Risoluzione suggerita indicata dal sistema di risoluzione dei conflitti per l'articolo.  
  
 **Autore**  
 Il valore di dati nel server di pubblicazione.  
  
 **Sottoscrittore**  
 Il valore di dati nel Sottoscrittore.  
  
 **Accetta soluzione proposta**, **Accetta server di pubblicazione**e **Accetta Sottoscrittore**  
 Fare clic su questo pulsante per accettare la riga che verrà applicata al server di pubblicazione o al Sottoscrittore, a seconda della riga che prevale nel conflitto. Se la riga del server di pubblicazione non viene confermata, tutti gli altri Sottoscrittori riceveranno la riga confermata durante la successiva sincronizzazione con il server di pubblicazione.  
  
 **Risoluzione automatica conflitti rimanenti**  
 Risolve tutti i conflitti rimanenti utilizzando la risoluzione suggerita indicata dal sistema di risoluzione dei conflitti per l'articolo.  
  
 **Registra informazioni dettagliate sul conflitto per riferimenti futuri**  
 Registra informazioni dettagliate sul conflitto nelle tabelle di sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione interattiva dei conflitti](merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Visualizzare e risolvere i conflitti di dati per le pubblicazioni di tipo merge &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows &#40;Gestione sincronizzazione Microsoft&#41;](synchronize-a-subscription-using-windows-synchronization-manager.md)   
 [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
