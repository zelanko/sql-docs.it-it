---
title: Associare un parametro di query a un parametro di report (Generatore report) | Microsoft Docs
description: Informazioni su come usare i parametri dei report di Reporting Services, sulle proprietà che è possibile impostare e su come associare un parametro di query del set di dati a un parametro del report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- queries [Reporting Services], parameters
- parameters [Reporting Services], queries
ms.assetid: 6d297e1a-ff71-472a-addc-349e863092b5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 76af4ebaaabf8b99f6bf654715aeb5e19791b3db
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85808471"
---
# <a name="associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs"></a>Associazione di un parametro di query a un parametro di report (Generatore report e SSRS)
  Quando si definisce una query del set di dati contenente una variabile di query, il comando della query viene analizzato. Per ogni variabile di query, vengono creati un parametro del set di dati e un parametro del report corrispondenti. Il parametro del set di dati punta al parametro del report. Questo consente di immettere un valore che viene passato direttamente alla query. Ogni volta che si modifica il comando della query, si verifica lo stesso processo.  
  
 Per rinominare un parametro di report associato a un parametro di query, è necessario collegare manualmente i parametri di query al parametro di report rinominato utilizzando la procedura illustrata in questo argomento.  
  
> **NOTA:** [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-associate-a-query-parameter-with-a-report-parameter"></a>Per associare un parametro di query a un parametro di report  
  
1.  Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sul set di dati, fare clic su **Proprietà set di dati**, quindi scegliere **Parametri**.  
  
    > **NOTA** Se il riquadro Dati report non è visualizzato, scegliere **Dati report** dal menu **Visualizza** .  
  
2.  Nella colonna **Nome parametro**individuare il nome del parametro di query. I nomi dei parametri vengono popolati automaticamente in base alla query. Ogni volta che si modifica la query, vengono verificati i nuovi parametri della query. I parametri di query creati manualmente non vengono modificati quando la query cambia.  
  
    -   In **Nome parametro**individuare il nome del parametro di query così come è riportato nella query. È anche possibile aggiungere manualmente un nuovo parametro di query e specificare un nome.  
  
    -   In **Valore parametro**digitare o selezionare un'espressione che restituisca il valore da passare al parametro di query. Si tratta in genere del nome del parametro di report.  
  
        > **NOTA** Non è obbligatorio utilizzare i parametri di report come valori per un parametro di query. È infatti possibile utilizzare qualsiasi espressione che restituisca un valore per il parametro.  
  
3.  Ripetere il passaggio 2 per gli altri parametri di query.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   

  
  
