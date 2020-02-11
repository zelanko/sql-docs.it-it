---
title: Visualizzare il piano di esecuzione stimato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 555ded0e34c0dc13ce794cc6f3119af7b2688910
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150878"
---
# <a name="display-the-estimated-execution-plan"></a>Visualizzazione del piano di esecuzione stimato
  In questo argomento viene descritta la procedura per generare rappresentazioni grafiche di piani di esecuzione stimati mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando si generano piani di esecuzione stimati, le query o i batch [!INCLUDE[tsql](../../includes/tsql-md.md)] non vengono eseguiti. Nel piano di esecuzione generato vengono invece visualizzate le query che verrebbero utilizzate con maggiore probabilità da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in caso di effettiva esecuzione.  
  
 Per utilizzare questa funzionalità, è necessario che gli utenti dispongano delle autorizzazioni appropriate relative all'esecuzione delle query [!INCLUDE[tsql](../../includes/tsql-md.md)] per le quali verrà generato un piano di esecuzione grafico, nonché dell'autorizzazione SHOWPLAN per tutti i database a cui fa riferimento la query.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Per visualizzare il piano di esecuzione stimato di una query  
  
1.  Sulla barra degli strumenti fare clic su **motore di database query**. Per aprire una query esistente e visualizzare il piano di esecuzione stimato, è anche possibile fare clic sul pulsante **Apri file** della barra degli strumenti e trovare la query.  
  
2.  Immettere la query di cui si desidera visualizzare il piano di esecuzione stimato.  
  
3.  Scegliere **Visualizza piano di esecuzione stimato** dal menu **Query** oppure fare clic sul pulsante **Visualizza piano di esecuzione stimato** della barra degli strumenti. Il piano di esecuzione stimato verrà visualizzato nel riquadro Risultati della scheda **Piano di esecuzione** . Per visualizzare informazioni aggiuntive, posizionare il mouse sulle icone degli operatori logici e fisici e visualizzare la descrizione e le proprietà dell'operatore nella descrizione comando. In alternativa, è possibile visualizzare le proprietà dell'operatore nella finestra Proprietà. Se tale finestra non è visibile, fare clic con il pulsante destro del mouse su un operatore e scegliere **Proprietà**. Selezionare un operatore e visualizzare le relative proprietà.  
  
4.  Per modificare la visualizzazione del piano di esecuzione, fare clic con il pulsante destro del mouse sul piano di esecuzione e scegliere **zoom avanti**, **Zoom indietro**, **Personalizza zoom**o **adatta alla**finestra. **Zoom avanti** e **Zoom indietro** consentono rispettivamente di ingrandire o ridurre il piano di esecuzione in base a valori di percentuale predefiniti. **Personalizza zoom** consente di definire un ingrandimento personalizzato per la visualizzazione, ad esempio 80 percento. **Adatta alla finestra consente** di ingrandire il piano di esecuzione per adattarlo al riquadro risultati.  
  
  
