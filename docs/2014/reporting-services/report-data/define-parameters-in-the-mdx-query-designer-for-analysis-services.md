---
title: Definizione di parametri in Progettazione query MDX per Analysis Services (Generatore report e SSRS) Documenti Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
manager: kfile
ms.openlocfilehash: 39f94bc7fd247a1608385f009fcb8d117b8c628f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388539"
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services-report-builder-and-ssrs"></a>Definizione dei parametri in Progettazione query MDX per Analysis Services (Generatore report e SSRS)
  Per parametrizzare una query MDX per un'origine dati di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , è necessario aggiungere un parametro di query alla query. In Progettazione query MDX, è possibile aggiungere un parametro di query sia in modalità progettazione sia in modalità query specificando un filtro. Dopo avere definito la query tramite un parametro di query, in Reporting Services vengono creati automaticamente un parametro di report e un set di dati per l'elenco dei valori validi. In questo modo un utente può specificare un valore che viene passato direttamente alla query.

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>Per definire un parametro di query MDX in modalità progettazione

1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su un set di dati creato da un tipo di origine dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e quindi scegliere **Query**. La finestra Progettazione query MDX verrà aperta in modalità progettazione.

2.  Trascinare una dimensione nell'area filtro e rilasciarla nella prima cella della colonna **Dimensione** .

3.  Selezionare un valore nell'elenco a discesa della colonna **Gerarchia** .

4.  Selezionare un operatore nell'elenco a discesa della colonna **Operatore** .

5.  Selezionare valori singoli nell'elenco a discesa della colonna **Espressione filtro** oppure fare clic sul membro **Totale** per selezionare tutti i valori.

6.  Selezionare la casella di controllo nella colonna **Parametri** per creare un parametro del report.

7.  Fare clic su **Esegui**.

     Dopo avere eseguito la query, fare clic su **Progettazione** nella barra degli strumenti per passare alla modalità query e visualizzare la query MDX creata. Non modificare il testo della query in modalità query se si desidera continuare a sviluppare la query in modalità progettazione. Fare clic su **Progettazione** per passare di nuovo alla modalità progettazione.

8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

     Nel riquadro dei dati del report espandere il nodo Parametri per visualizzare il parametro del report creato automaticamente per il filtro.

     Per visualizzare il set di dati dei valori disponibili per il parametro del report, fare clic con il pulsante destro del mouse su un'area vuota nel riquadro Dati report e selezionare **Mostra set di dati nascosti**. Nel riquadro dei dati del report verranno visualizzati tutti i set di dati contenuti nel report.

### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>Per definire un parametro di query MDX in modalità query

1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su un set di dati creato da un tipo di origine dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e quindi scegliere **Query**. La finestra Progettazione query MDX verrà aperta in modalità progettazione.

2.  Fare clic su **Progettazione** nella barra degli strumenti per passare alla modalità query.

3.  Nella barra degli strumenti della progettazione query MDX fare clic su **Parametri query** (![icona della finestra di dialogo Parametri query](../../analysis-services/media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")). Verrà visualizzata la finestra di dialogo Parametri query.

4.  Nella colonna **Parametro** selezionare **\<Immetti parametro>** e digitare il nome di un parametro.

5.  Selezionare un valore nell'elenco a discesa della colonna **Dimensione** .

6.  Selezionare un valore nell'elenco a discesa della colonna **Gerarchia** .

7.  Selezionare la casella di controllo nella colonna **Più valori** per creare un parametro multivalore.

8.  Nell'elenco a discesa della colonna **Predefinito** selezionare uno o più valori a seconda della selezione eseguita nel passaggio 5.

9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

10. Nella barra degli strumenti Progettazione query fare clic su **Esegui**.

11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

     Nel riquadro dei dati del report espandere il nodo Parametri per visualizzare il parametro del report creato automaticamente per il filtro.

     Per visualizzare il set di dati dei valori disponibili per il parametro del report, fare clic con il pulsante destro del mouse su un'area vuota nel riquadro Dati report e selezionare **Mostra set di dati nascosti**. Nel riquadro dei dati del report verranno visualizzati tutti i set di dati contenuti nel report.

## <a name="see-also"></a>Vedere anche
 [Tipo di connessione di Analysis Services per l'interfaccia](analysis-services-connection-type-for-mdx-ssrs.md) utente di Progettazione query MDX &#40;SSRS&#41;[Analysis Services](analysis-services-mdx-query-designer-user-interface.md)


