---
title: Specifica del tipo di dati e del tipo di contenuto (esercitazione di base sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62720049"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Impostazione del tipo di dati e contenuto (Esercitazione di base sul data mining)
  Ora che sono state selezionate le colonne da utilizzare per la compilazione della struttura e il training dei modelli, apportare le modifiche necessarie ai tipi di dati e di contenuto predefiniti impostati dalla procedura guidata.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Esaminare e modificare il tipo di contenuto e di dati per ogni colonna  
  
1.  Nella pagina **impostazione tipo di contenuto e dati delle colonne** fare clic su **rileva** per eseguire un algoritmo che determina i dati predefiniti e i tipi di contenuto per ogni colonna.  
  
2.  Esaminare le voci nelle colonne **tipo di contenuto** e **tipo di dati** e modificarle, se necessario, per assicurarsi che le impostazioni corrispondano a quelle elencate nella tabella seguente.  
  
     In genere, la procedura guidata rileva i numeri e assegna un tipo di dati numerico adatto, ma esistono diversi scenari in cui è invece necessario gestire un numero come testo. Ad esempio, il **GeographyKey** deve essere gestito come testo, perché non sarebbe appropriato eseguire operazioni matematiche su questo identificatore.  
  
    |Colonna|Content Type|Tipo di dati|  
    |------------|------------------|---------------|  
    |**Indirizzo riga 1**|**Discrete**|**Text**|  
    |**Indirizzo Riga2**|**Discrete**|**Text**|  
    |**Età**|**Continuo**|**long**|  
    |**Bike Buyer**|**Discrete**|**long**|  
    |**Commute Distance**|**Discrete**|**Text**|  
    |**CustomerKey**|**Codice**|**long**|  
    |**DateLastPurchase**|**Continuo**|**Data**|  
    |**Indirizzo di posta elettronica**|**Discrete**|**Text**|  
    |**English Education**|**Discrete**|**Text**|  
    |**English Occupation**|**Discrete**|**Text**|  
    |**FirstName**|**Discrete**|**Text**|  
    |**Genere**|**Discrete**|**Text**|  
    |**Geography Key**|**Discrete**|**Text**|  
    |**House Owner Flag**|**Discrete**|**Text**|  
    |**Cognome**|**Discrete**|**Text**|  
    |**Marital Status**|**Discrete**|**Text**|  
    |**Number Cars Owned**|**Discrete**|**long**|  
    |**Numero di figli a casa**|**Discrete**|**long**|  
    |**Area**|**Discrete**|**Text**|  
    |**Total Children**|**Discrete**|**long**|  
    |**Yearly Income**|**Continuo**|**Double**|  
  
3.  Fare clic su **Avanti**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Specifica di un set di dati di testing per la struttura &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di una struttura del modello di data mining Targeted Mailing &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Tipi di contenuto &#40;&#41;di data mining](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipi di dati &#40;Data mining&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
