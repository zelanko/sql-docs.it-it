---
title: 'Lezione 3: Rinominare le colonne | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80d9cae6deae4059327084f531f6a6d958a39ec6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070323"
---
# <a name="lesson-3-rename-columns"></a>Lezione 3: Rinominare colonne
  In questa lezione verranno rinominate numerose colonne di ogni tabella importata. La ridenominazione semplifica l'identificazione e l'esplorazione delle colonne, sia in Progettazione di modelli che da parte degli utenti che selezionano campi in un'applicazione client. Per altre informazioni, vedere [Rinominare una tabella o una colonna &#40;SSAS tabulare&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
>  La ridenominazione delle colonne non è necessaria per completare questa esercitazione. Nelle lezioni successive, in particolare in quelle che prevedono la creazione di relazioni e di colonne e misure calcolate utilizzando formule DAX, viene tuttavia fatto riferimento ai nomi descrittivi delle colonne indicati in questa lezione. Se si sceglie di non rinominare le colonne, sarà necessario modificare le formule DAX nelle lezioni 5, 6 e 7 per utilizzare i nomi originali delle colonne di origine forniti in questa lezione.  
  
 Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 2: Aggiungere dati](lesson-2-add-data.md).  
  
## <a name="rename-columns"></a>Rinominare colonne  
  
#### <a name="to-rename-columns"></a>Per rinominare colonne  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
     Quando si fa clic su una scheda, tale tabella diventa attiva nella finestra di Progettazione modelli.  
  
2.  Fare doppio clic il **CustomerKey** colonna nome, quindi digitare `Customer  Id`, quindi premere INVIO.  
  
    > [!TIP]  
    >  È anche possibile rinominare una colonna nel **nome della colonna** proprietà della colonna **proprietà** finestra o nella vista diagramma.  
  
3.  Rinominare le colonne rimanenti della tabella **Customer** e le colonne delle tabelle rimanenti, sostituendo il nome di origine con il nome descrittivo:  
  
     **Tabella Customer**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |FirstName|Nome|  
    |MiddleName|Middle Name|  
    |LastName|Cognome|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Address Line 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Commute Distance|  
  
     **Data**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|Date|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
     **Geography**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|ID territorio vendita|  
  
     **Product**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|Nome prodotto|  
    |StandardCost|Standard Cost|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|List Price|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Dealer Price|Dealer Price|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|Descrizione|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |Stato|Product Status|  
  
     **Categoria di prodotto**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **Sottocategoria di prodotto**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
     **Internet Sales**  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|ID territorio vendita|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|Revision Number|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Unit Price|  
    |ExtendedAmount|Extended Amount|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Discount Amount|  
    |ProductStandardCost|Product Standard Cost|  
    |TotalProductCost|Total Product Cost|  
    |SalesAmount|Sales Amount|  
    |TaxAmt|Tax Amt|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>Passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 4: Contrassegna come tabella data](lesson-3-mark-as-date-table.md).  
  
  
