---
title: Finestra di dialogo Proprietà set di dati, Parametri | Microsoft Docs
description: Informazioni sull'uso della proprietà Parametri nella finestra di dialogo Proprietà set di dati per aggiungere, cambiare ed eliminare parametri di query.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: reference
f1_keywords:
- "10150"
- sql13.rtp.rptdesigner.datasetproperties.parameters.f1
- "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fc0f85dbd100593549ab3f543dfaf4f95e0d91ba
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812242"
---
# <a name="dataset-properties-dialog-box-parameters"></a>Finestra di dialogo Proprietà set di dati, Parametri
  Selezionare **Parametri** nella finestra di dialogo **Proprietà set di dati** per aggiungere, modificare ed eliminare parametri di query, inclusi quelli collegati a parametri del report.  
  
 Ogni volta che la query viene modificata nella relativa scheda, il comando della query viene analizzato. Per ogni parametro di query identificato, viene creato un parametro del report con un nome identico con distinzione tra maiuscole e minuscole. Per impostazione predefinita, il parametro di query viene aggiunto automaticamente all'elenco dei parametri di query e collegato al parametro del report corrispondente.  
  
 In caso di dipendenze dei valori predefiniti di un parametro del report da un altro parametro del report collegato a un parametro di query, l'ordine dei parametri del report visualizzati nella finestra di dialogo **Proprietà parametri report** risulta importante. I parametri del report che vengono dopo nell'elenco possono fare riferimento a parametri che vengono prima. Per altre informazioni sui parametri report, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="options"></a>Opzioni  
 **Aggiungere**  
 Consente di aggiungere un nuovo parametro all'elenco.  
  
 **Elimina**  
 Consente di rimuovere il parametro selezionato dall'elenco.  
  
 **Nome parametro**  
 Digitare il nome di un parametro di query aggiunto al set di dati nella scheda **Query** della finestra di dialogo **Proprietà set di dati** .  
  
 **Valore del parametro**  
 Immettere un valore per il parametro di query. Può trattarsi di un valore statico o di un'espressione che fa riferimento a un oggetto nel report, ma non a un campo o a un elemento del report. Per impostazione predefinita, in **Valore** è contenuta un'espressione che punta a un parametro del report.  
  
 **Freccia in su**  
 Consente di spostare il parametro selezionato verso l'alto nell'elenco.  
  
 **Freccia GIÙ**  
 Consente di spostare il parametro selezionato verso il basso nell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Modificare l'ordine di un parametro del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
