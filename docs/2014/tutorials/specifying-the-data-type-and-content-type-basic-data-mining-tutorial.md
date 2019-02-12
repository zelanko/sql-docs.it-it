---
title: Specifica il tipo di dati e il tipo di contenuto (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040203"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Impostazione del tipo di dati e contenuto (Esercitazione di base sul data mining)
  Ora che sono state selezionate le colonne da utilizzare per la compilazione della struttura e il training dei modelli, apportare le modifiche necessarie ai tipi di dati e di contenuto predefiniti impostati dalla procedura guidata.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Esaminare e modificare il tipo di contenuto e di dati per ogni colonna  
  
1.  Nel **contenuto e tipo di dati specificare colonne** pagina, fare clic su **rileva** per eseguire un algoritmo che determina i dati predefiniti e i tipi di contenuto per ogni colonna.  
  
2.  Esaminare le voci nel **tipo di contenuto** e **tipo di dati** colonne e modificarli se necessario, per assicurarsi che le impostazioni siano identici a quelli elencati nella tabella seguente.  
  
     In genere, la procedura guidata rileva i numeri e assegna un tipo di dati numerico adatto, ma esistono diversi scenari in cui è invece necessario gestire un numero come testo. Ad esempio, il **GeographyKey** deve essere gestita come testo, perché non è corretto eseguire operazioni matematiche su questo identificatore.  
  
    |colonna|Tipo di contenuto|Tipo di dati|  
    |------------|------------------|---------------|  
    |**Riga indirizzo 1**|**Discreta**|**per**|  
    |**Riga indirizzo 2**|**Discreta**|**per**|  
    |**Età**|**continua**|**Long**|  
    |**Bike Buyer**|**Discreta**|**Long**|  
    |**Commute Distance**|**Discreta**|**per**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**continua**|**Data**|  
    |**Email Address**|**Discreta**|**per**|  
    |**English Education**|**Discreta**|**per**|  
    |**English Occupation**|**Discreta**|**per**|  
    |**FirstName**|**Discreta**|**per**|  
    |**Gender**|**Discreta**|**per**|  
    |**Geography Key**|**Discreta**|**per**|  
    |**House Owner Flag**|**Discreta**|**per**|  
    |**Last Name**|**Discreta**|**per**|  
    |**Marital Status**|**Discreta**|**per**|  
    |**Number Cars Owned**|**Discreta**|**Long**|  
    |**Number Children At Home**|**Discreta**|**Long**|  
    |**Region**|**Discreta**|**per**|  
    |**Total Children**|**Discreta**|**Long**|  
    |**Yearly Income**|**continua**|**Double**|  
  
3.  Scegliere **Avanti**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Specifica un Set di dati di Testing per la struttura &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di una struttura modello di Data Mining Targeted Mailing &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipi di dati &#40;Data mining&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
