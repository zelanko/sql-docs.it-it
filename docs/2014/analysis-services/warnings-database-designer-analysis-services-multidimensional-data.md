---
title: Avvisi (progettazione Database) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90eeca203c672c21551b8aff2e24feb164d8fda5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065431"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>Avvisi (Progettazione database) (Analysis Services - Dati multidimensionali)
  Usare la scheda **Avvisi** per visualizzare e ignorare totalmente le regole e per visualizzare e riattivare istanze specifiche di avvisi ignorati. Il **avvisi** scheda Visualizza due griglie: **Regole per gli avvisi di progettazione** e **avvisi ignorati**.  
  
 **Per visualizzare la scheda avvisi**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire un progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , fare clic su **Modifica database**e quindi sulla scheda **Avvisi** .  
  
## <a name="design-warning-rules-grid"></a>Griglia Regole per gli avvisi di progettazione  
 La griglia **Regole per gli avvisi di progettazione** visualizza tutte le regole dell'avviso di progettazione. Questa griglia controlla anche quali regole sono attivate nel database. Per attivare o disabilitare una regola dell'avviso, selezionare o deselezionare la casella di controllo.  
  
 La griglia **Regole per gli avvisi di progettazione** ha le seguenti colonne:  
  
 **Descrizione**  
 Visualizza il nome della regola. Le regole sono raggruppate per categoria.  
  
 **Priorità**  
 Visualizza la priorità assegnata alla regola.  
  
 **Commenti**  
 (Facoltativo) Consente all'utente di digitare un commento che spieghi perché si sta ignorando l'avviso.  
  
## <a name="dismissed-warnings-grid"></a>Griglia Avvisi ignorati  
 La griglia **Avvisi ignorati** visualizza tutte le occorrenze specifiche dell'avviso ignorate dall' **Elenco errori**. Per riattivare un avviso, selezionarlo nella griglia, quindi fare clic su **Riabilita**.  
  
 La griglia **Avvisi ignorati** ha i seguenti elementi :  
  
 **Oggetto**  
 Visualizza un'icona che rappresenta il tipo di oggetto e il nome dell'oggetto.  
  
 **Tipo**  
 Visualizza il tipo di oggetto.  
  
 **Descrizione**  
 Visualizza il nome della regola.  
  
 **Priorità**  
 Visualizza la priorità assegnata alla regola.  
  
 **Commenti**  
 Visualizza il commento immesso quando l'avviso è stato ignorato. Qui è possibile aggiungere o modificare un commento.  
  
 **Abilitare di nuovo**  
 Riattiva gli avvisi selezionati.  
  
> [!NOTE]  
>  Se un oggetto ha un avviso, ma è in uno stato non valido o è stato rimosso manualmente dal progetto, verrà visualizzata un'icona Errori nell'elenco accanto all'avviso. Per ignorare l'avviso, selezionarlo, quindi fare clic su **Riabilita**.  
  
## <a name="see-also"></a>Vedere anche  
 [Chiudere la finestra di dialogo di avviso &#40;Analysis Services - dati multidimensionali&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [Generale &#40;finestra di progettazione del Database&#41; &#40;Analysis Services - dati multidimensionali&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
