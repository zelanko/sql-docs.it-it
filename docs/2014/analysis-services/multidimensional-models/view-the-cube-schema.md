---
title: Visualizzare lo Schema del cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 93898e6ed8dc26e3b06fd6a583bfa4084dd4c5f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740691"
---
# <a name="view-the-cube-schema"></a>Visualizzare lo schema del cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Lo schema del cubo viene visualizzato nel riquadro **Vista origine dati** della scheda **Struttura cubo** in **Progettazione cubi** . Lo schema è il set di tabelle da cui derivano le misure e le dimensioni per un cubo. Ogni schema del cubo è costituito da una o più tabelle dei fatti e da una o più tabelle delle dimensioni su cui sono basate le misure e le dimensioni nel cubo.  
  
 Nel riquadro **Vista origine dati** della scheda **Struttura cubo** viene visualizzato un diagramma vista origine dati su cui è basato il cubo. Questo diagramma è un subset del diagramma principale della vista origine dati. È possibile nascondere e mostrare tabelle nel riquadro **Vista origine dati** , nonché visualizzare tutti i diagrammi esistenti. Tuttavia, non è possibile apportare modifiche, ad esempio aggiungere nuove relazioni o query denominate, allo schema sottostante. Per apportare modifiche allo schema, utilizzare Progettazione vista origine dati.  
  
 Quando si crea un cubo, il diagramma visualizzato nel riquadro **Vista origine dati** della scheda **Struttura cubo** corrisponde inizialmente al diagramma **Mostra tutte le tabelle** nella vista origine dati per il progetto o il database. È possibile sostituire questo diagramma con uno esistente nella vista origine dati e apportare modifiche nel riquadro **Vista origine dati** .  
  
 Mentre si utilizza il diagramma in **Progettazione cubi**, i comandi che agiscono sulla scheda o su qualsiasi oggetto selezionato nella scheda sono disponibili nel menu **Vista origine dati** . È anche possibile fare clic con il pulsante destro del mouse sullo sfondo del diagramma o su qualsiasi oggetto nel diagramma per utilizzare i comandi che agiscono sul diagramma o sull'oggetto selezionato. È possibile effettuare le operazioni seguenti:  
  
-   Passare dal formato diagramma a quello ad albero.  
  
-   Disporre, trovare, mostrare e nascondere tabelle.  
  
-   Mostrare nomi descrittivi.  
  
-   Cambiare layout.  
  
-   Modificare l'ingrandimento.  
  
-   Visualizzare proprietà.  
  
 Inoltre, è possibile effettuare le azioni elencate nella tabella seguente:  
  
|Per|Procedere nel modo seguente|  
|--------|-------------|  
|Utilizzare un diagramma dalla vista origine dati del cubo|Selezionare **Copia diagramma da** nel menu **Vista origine dati**, quindi fare clic sul diagramma vista origine dati da usare.<br /><br /> - oppure -<br /><br /> Fare clic con il pulsante destro del mouse sullo sfondo del riquadro **Vista origine dati** , scegliere **Copia diagramma da**, quindi fare clic sul diagramma desiderato nella vista origine dati. Questo metodo consente di creare una copia indipendente del diagramma, pertanto tutte le modifiche apportate alla scheda **Generatore cubi** non vengono visualizzate nel diagramma originale.|  
|Mostrare solo le tabelle utilizzate nel cubo|Scegliere **Mostra solo tabelle utilizzate** dal menu **Vista origine dati**.<br /><br /> - oppure -<br /><br /> Fare clic con il pulsante destro del mouse sullo sfondo del riquadro **Vista origine dati** , quindi scegliere **Mostra solo tabelle utilizzate**.|  
|Modificare lo schema della vista origine dati|Scegliere **Modifica vista origine dati** dal menu **Vista origine dati**.<br /><br /> - oppure -<br /><br /> Fare clic con il pulsante destro del mouse sullo sfondo del riquadro **Vista origine dati** , quindi scegliere **Modifica vista origine dati**.|  
  
  
