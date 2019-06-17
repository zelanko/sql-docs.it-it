---
title: Importa da un'origine dati multidimensionale (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 666b7fdf5af10b6726a1e1d7a2aaafa075bf8777
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080561"
---
# <a name="import-from-a-multidimensional-data-source-ssas-tabular"></a>Importare da un'origine dati multidimensionale (SSAS tabulare)
  Un database del cubo di Analysis Services può essere utilizzato come origine dati per un modello tabulare. Per importare dati da un cubo di Analysis Services, è necessario definire una query MDX per selezionare i dati da importare.  
  
 È possibile importare in un modello qualsiasi tipo di dati contenuto in un database di SQL Server Analysis Services. È possibile estrarre tutta o parte di una dimensione oppure ottenere sezioni e funzioni di aggregazione dal cubo, ad esempio la somma mensile delle vendite per l'anno corrente, e così via. È tuttavia necessario tenere presente che tutti i dati importati da un cubo sono bidimensionali. Se pertanto si definisce una query che consente di recuperare misure in base a più dimensioni, ogni dimensione dei dati verrà importata in una colonna separata.  
  
 La versione dei cubi di Analysis Services deve essere SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>Per importare dati da un cubo di Analysis Services  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**.  
  
2.  Selezionare **Microsoft Analysis Services** nella pagina **Connessione a un'origine dati**, quindi scegliere **Avanti**.  
  
3.  Seguire i passaggi nell'Importazione guidata tabella. Sarà possibile specificare una query MDX nella pagina **Specifica di una query MDX** . Per utilizzare Progettazione query MDX, nella pagina Specifica di una query MDX fare clic su **Progettazione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Importare dati &#40;SSAS tabulare&#41;](import-data-ssas-tabular.md)   
 [Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
