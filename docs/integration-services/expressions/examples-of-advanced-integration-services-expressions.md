---
title: Esempi di espressioni avanzate di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dbf2c304cf97dfad85fbdb53ca83fd7922e3a128
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917655"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>Esempi di espressioni avanzate di Integration Services

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  In questa sezione vengono forniti esempi di alcune funzioni avanzate, in cui sono combinati più operatori e funzioni. Le espressioni utilizzate nei vincoli di precedenza o nella trasformazione Suddivisione condizionale devono restituire un valore booleano. Tale restrizione non si applica tuttavia alle espressioni utilizzate in espressioni di proprietà e variabili, nella trasformazione Colonna derivata o nel contenitore Ciclo For.  
  
 Gli esempi seguenti usano i database **AdventureWorks** e [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ogni esempio viene indicata la tabella utilizzata.  
  
## <a name="boolean-expressions"></a>Espressioni booleane  
  
-   Questo esempio usa la tabella **Product** . L'espressione valuta la voce del mese nella colonna **SellStartDate** e restituisce TRUE se il mese è giugno o uno successivo.  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   Questo esempio usa la tabella **Product** . L'espressione valuta il risultato arrotondato della divisione della colonna **ListPrice** per la colonna **StandardCost** e restituisce TRUE se questo risultato è maggiore di 1,5.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   Questo esempio usa la tabella **Product** . L'espressione restituisce TRUE se tutte e tre le operazioni restituiscono TRUE. Se la colonna **Size** e la variabile **BikeSize** hanno tipi di dati incompatibili, l'espressione richiederà un cast esplicito, come mostrato nel secondo esempio. Il cast a DT_WSTR include la lunghezza della stringa.  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   Questo esempio usa la tabella **CurrencyRate** . L'espressione confronta valori in tabelle e variabili. Restituisce TRUE se la voce nella colonna **FromCurrencyCode** o **ToCurrencyCode** è uguale al valore della variabile e se il valore in **AverageRate** è maggiore del valore in **EndOfDayRate**.  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   Questo esempio usa la tabella **Currency** . L'espressione restituisce TRUE se il primo carattere nella colonna **Name** non è a o A.  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     L'espressione seguente restituisce gli stessi risultati ma è più efficiente, perché viene convertito in maiuscolo un solo carattere.  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>Espressioni non booleane  
 Le espressioni non booleane vengono utilizzate nella trasformazione Colonna derivata, nelle espressioni di proprietà e nel contenitore Ciclo For.  
  
-   Questo esempio usa la tabella **Contact** . L'espressione rimuove gli spazi iniziali e finali dalle colonne **FirstName**, **MiddleName**e **LastName** . Estrae la prima lettera della colonna **MiddleName** se non è Null, concatena l'iniziale del secondo nome e i valori in **FirstName** e **LastName**e inserisce gli spazi appropriati tra i valori.  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   Questo esempio usa la tabella **Contact** . L'espressione convalida le voci nella colonna **Salutation** . Restituisce una voce di **Salutation** o una stringa vuota.  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   Questo esempio usa la tabella **Product** . L'espressione converte in maiuscolo il primo carattere nella colonna **Color** e in minuscolo i caratteri rimanenti.  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   Questo esempio usa la tabella **Product** . L'espressione calcola il numero dei mesi per cui un determinato prodotto è stato venduto e restituisce la stringa "Unknown" se la colonna **SellStartDate** o **SellEndDate** contiene NULL.  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   Questo esempio usa la tabella **Product** . L'espressione calcola il margine di profitto sulla colonna **StandardCost** e arrotonda il risultato alla precisione 2. Il risultato viene presentato come percentuale.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>Attività correlate  
 [Usare un'espressione in un componente flusso di dati](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=746575)sul sito Web pragmaticworks.com  
  
  
