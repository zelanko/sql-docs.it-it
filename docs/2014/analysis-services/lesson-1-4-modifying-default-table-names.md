---
title: Modifica di nomi di tabella predefinito | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82f448c652bfb36f0f09eba975e3fecd8915afab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729541"
---
# <a name="modifying-default-table-names"></a>Modifica dei nomi predefiniti delle tabelle
  È possibile modificare il valore della proprietà **FriendlyName** per gli oggetti nella vista origine dati per renderli più semplici da individuare e usare.  
  
 Nell'attività seguente si modificherà il nome descrittivo di ogni tabella nella vista origine dati rimuovendo da tali tabelle i prefissi "**Dim**" e "**Fact**". In questo modo, gli oggetti cubo e dimensione, che verranno definiti nella lezione successiva, risulteranno più semplici da individuare e utilizzare.  
  
> [!NOTE]  
>  È inoltre possibile modificare i nomi descrittivi delle colonne, definire colonne calcolate e unire in join tabelle o viste della vista origine dati per semplificarne l'utilizzo.  
  
### <a name="to-modify-the-default-name-of-a-table"></a>Per modificare il nome predefinito di una tabella  
  
1.  Nel riquadro **Tabelle** di **Progettazione vista origine dati**fare clic con il pulsante destro del mouse sulla tabella **FactInternetSales** e quindi scegliere **Proprietà**.  
  
2.  Se la finestra Proprietà non è visualizzata sul lato destro della finestra di Microsoft Visual Studio, fare clic sul pulsante **Nascondi automaticamente** sulla barra del titolo della finestra Proprietà in modo che la finestra rimanga visibile.  
  
     Se la finestra Proprietà rimane aperta è più facile modificare le proprietà di ogni tabella della vista origine dati. Se la finestra non viene tenuta aperta usando il pulsante **Nascondi automaticamente** , si chiuderà quando si fa clic su un altro oggetto nel riquadro **Diagramma** .  
  
3.  Modifica il **FriendlyName** proprietà per il **FactInternetSales** oggetto *`InternetSales`*.  
  
     La modifica viene applicata quando si fa clic in un punto diverso dalla cella della proprietà **FriendlyName** . Nella lezione successiva si definirà un gruppo di misure basato su questa tabella dei fatti. Il nome della tabella dei fatti sarà InternetSales anziché FactInternetSales a causa della modifica apportata in questa lezione.  
  
4.  Fare clic su **DimProduct** nel riquadro **Tabelle** . Nella finestra Proprietà modificare il **FriendlyName** proprietà *`Product`*.  
  
5.  Modificare la proprietà **FriendlyName** delle tabelle rimanenti nella vista origine dati allo stesso modo per rimuovere il prefisso "**Dim**".  
  
6.  Al termine fare di nuovo clic sul pulsante **Nascondi automaticamente** per nascondere la finestra Proprietà.  
  
7.  Scegliere **Salva tutti** dal menu [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]File **o sulla barra degli strumenti di** per salvare le modifiche apportate fino a questo punto al progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. Se si desidera, è possibile arrestare l'esercitazione e riprenderla in seguito.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Definizione e distribuzione di un cubo](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Modificare le proprietà in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
