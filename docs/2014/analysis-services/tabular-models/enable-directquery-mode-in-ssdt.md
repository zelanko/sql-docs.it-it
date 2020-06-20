---
title: Abilitare la modalità di progettazione DirectQuery (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1387b5773ee3521979a3afc18f3417cabc156fe4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938922"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>Abilitare la modalità DirectQuery (SSAS tabulare)
  Per creare un modello in modalità DirectQuery, è innanzitutto necessario modificare l'ambiente di progettazione in modo che supporti l'utente della modalità DirectQuery. Quando si esegue questa operazione, vengono anche eseguite le operazioni seguenti:  
  
-   Abilitazione dell'utilizzo delle proprietà di distribuzione DirectQuery.  
  
-   Modifica del database dell'area di lavoro affinché venga eseguito in una modalità ibrida che utilizza la cache per la progettazione. Quando si distribuisce il modello, la modalità verrà nuovamente impostata sul valore specificato nelle proprietà di distribuzione del progetto.  
  
-   Disabilitazione delle caratteristiche di progettazione incompatibili con la modalità DirectQuery.  
  
-   Convalida del modello esistente.  
  
 Questa procedura descrive come abilitare la modalità DirectQuery nella finestra di progettazione.  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>Per abilitare l'utilizzo di DirectQuery in un modello  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il file della soluzione.  
  
2.  In Esplora oggetti fare doppio clic sul file Model.bim.  
  
3.  Nel riquadro **Proprietà** impostare la proprietà **DirectQueryMode**su **Attivato**.  
  
4.  In caso di errori, in Visual Studio aprire il **Elenco errori** e risolvere eventuali problemi che impediscono il passaggio del modello alla modalità DirectQuery.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery &#40;SSAS tabulare&#41;](directquery-mode-ssas-tabular.md)  
  
  
