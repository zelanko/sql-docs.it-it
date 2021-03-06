---
title: Definizione dei parametri in Progettazione query MDX per Analysis Services | Microsoft Docs
description: Informazioni su come definire i parametri di query in Progettazione query MDX (Multidimensional Expression) per Analysis Services.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 72fe1a64e1aa474d0aa0233e8065cf351acfe432
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458198"
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services"></a>Definizione dei parametri in Progettazione query MDX per Analysis Services
  Per parametrizzare una query MDX per un'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è necessario aggiungere un parametro di query alla query. In Progettazione query MDX, è possibile aggiungere un parametro di query sia in modalità progettazione sia in modalità query specificando un filtro. Dopo avere definito la query tramite un parametro di query, in Reporting Services vengono creati automaticamente un parametro di report e un set di dati per l'elenco dei valori validi. In questo modo un utente può specificare un valore che viene passato direttamente alla query.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>Per definire un parametro di query MDX in modalità progettazione  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su un set di dati creato da un tipo di origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Query**. La finestra Progettazione query MDX verrà aperta in modalità progettazione.  
  
2.  Trascinare una dimensione nell'area filtro e rilasciarla nella prima cella della colonna **Dimensione** .  
  
3.  Selezionare un valore nell'elenco a discesa della colonna **Gerarchia** .  
  
4.  Selezionare un operatore nell'elenco a discesa della colonna **Operatore** .  
  
5.  Selezionare valori singoli nell'elenco a discesa della colonna **Espressione filtro** oppure fare clic sul membro **Totale** per selezionare tutti i valori.  
  
6.  Selezionare la casella di controllo nella colonna **Parametri** per creare un parametro del report.  
  
7.  Fare clic su **Esegui**.  
  
     Dopo avere eseguito la query, fare clic su **Progettazione** nella barra degli strumenti per passare alla modalità query e visualizzare la query MDX creata. Non modificare il testo della query in modalità query se si desidera continuare a sviluppare la query in modalità progettazione. Fare clic su **Progettazione** per passare di nuovo alla modalità progettazione.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nel riquadro dei dati del report espandere il nodo Parametri per visualizzare il parametro del report creato automaticamente per il filtro.  
  
     Per visualizzare il set di dati dei valori disponibili per il parametro del report, fare clic con il pulsante destro del mouse su un'area vuota nel riquadro Dati report e selezionare **Mostra set di dati nascosti**. Nel riquadro dei dati del report verranno visualizzati tutti i set di dati contenuti nel report.  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>Per definire un parametro di query MDX in modalità query  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su un set di dati creato da un tipo di origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e quindi scegliere **Query**. La finestra Progettazione query MDX verrà aperta in modalità progettazione.  
  
2.  Fare clic su **Progettazione** nella barra degli strumenti per passare alla modalità query.  
  
3.  Nella barra degli strumenti della progettazione query MDX fare clic su **Parametri query** (![icona della finestra di dialogo Parametri query](../../reporting-services/report-data/media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")). Verrà visualizzata la finestra di dialogo Parametri query.  
  
4.  Nella colonna **Parametro** fare clic su **\<Enter Parameter>** e digitare il nome di un parametro.  
  
5.  Selezionare un valore nell'elenco a discesa della colonna **Dimensione** .  
  
6.  Selezionare un valore nell'elenco a discesa della colonna **Gerarchia** .  
  
7.  Selezionare la casella di controllo nella colonna **Più valori** per creare un parametro multivalore.  
  
8.  Nell'elenco a discesa della colonna **Predefinito** selezionare uno o più valori a seconda della selezione eseguita nel passaggio 5.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Nella barra degli strumenti Progettazione query fare clic su **Esegui**.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Nel riquadro dei dati del report espandere il nodo Parametri per visualizzare il parametro del report creato automaticamente per il filtro.  
  
     Per visualizzare il set di dati dei valori disponibili per il parametro del report, fare clic con il pulsante destro del mouse su un'area vuota nel riquadro Dati report e selezionare **Mostra set di dati nascosti**. Nel riquadro dei dati del report verranno visualizzati tutti i set di dati contenuti nel report.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di connessione Analysis Services per MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [Interfaccia utente di Progettazione query MDX di Analysis Services](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
  
