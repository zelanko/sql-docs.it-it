---
title: Introduzione alle dimensioni (dati multidimensionali Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2dce25d6638c5ec921ec22601ed73d03a2ccb215
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887865"
---
# <a name="introduction-to-dimensions-analysis-services---multidimensional-data"></a>Introduzione alle dimensioni (Analysis Services - Dati multidimensionali)
  Tutte le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dimensioni di Microsoft [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono gruppi di attributi basati su colonne di tabelle o viste in una vista origine dati. Le dimensioni esistono indipendentemente da un cubo, possono essere utilizzate in più cubi, possono essere utilizzate più volte in un singolo cubo e possono essere collegate tra istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Una dimensione indipendente da un cubo viene denominata dimensione del database e un'istanza di una dimensione del database all'interno di un cubo viene denominata dimensione del cubo.  
  
## <a name="dimension-based-on-a-star-schema-design"></a>Dimensione basata su una progettazione con schema star  
 La struttura di una dimensione è per lo più determinata dalla struttura della tabella della dimensione o delle tabelle delle dimensioni sottostanti. La struttura più semplice è detta schema star, dove ogni dimensione è basata su un'unica tabella delle dimensioni direttamente collegata alla tabella dei fatti tramite una relazione chiave primaria/chiave esterna.  
  
 Nel diagramma seguente viene illustrata una sottosezione del database [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] di esempio, in cui la tabella dei fatti **FactResellerSales** è correlata a due tabelle delle dimensioni, **DimReseller** e **DimPromotion**. La colonna **ResellerKey** nella tabella dei fatti **FactResellerSales** definisce una relazione di chiave esterna con la colonna chiave primaria **ResellerKey** nella tabella della dimensione **DimReseller** . Analogamente, la colonna **PromotionKey** nella tabella dei fatti **FactResellerSales** definisce una relazione di chiave esterna con la colonna chiave primaria **PromotionKey** nella tabella della dimensione **DimPromotion** .  
  
 ![Schema logico per la relazione tra dimensioni dei fatti](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimfactrelationship.gif "Schema logico per la relazione tra dimensioni dei fatti")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>Dimensione basata su una progettazione con schema snowflake  
 Spesso è necessaria una struttura più complessa in quanto per definire la dimensione sono necessarie informazioni di più tabelle. In questa struttura, denominata schema snowflake, ogni dimensione è basata su attributi di colonne di più tabelle collegate reciprocamente e alla tabella dei fatti tramite relazioni tra chiave primaria e chiave esterna. Nel diagramma seguente, ad esempio, vengono illustrate le tabelle necessarie per descrivere completamente la dimensione Product nel progetto di esempio **AdventureWorksDW** :  
  
 ![Tabella per la dimensione Product di adventureworkss](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimproduct.gif "Tabella per la dimensione Product di adventureworkss")  
  
 Per descrivere completamente un prodotto, la categoria e la sottocategoria del prodotto devono essere incluse nella dimensione Product. Tuttavia, tali informazioni non si trovano direttamente nella tabella principale per la dimensione **DimProduct** . Una relazione di chiave esterna da **DimProduct** a **DimProductSubcategory**, che a sua volta ha una relazione di chiave esterna con la tabella **DimProductCategory** , consente di includere le informazioni per le categorie di prodotti e sottocategorie della dimensione Product.  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>Confronto tra schema snowflake e relazione di tipo Riferimento  
 È talvolta possibile scegliere tra l'utilizzo di uno schema snowflake per definire gli attributi in una dimensione da più tabelle o l'utilizzo di due dimensioni separate definendo una relazione di tipo Riferimento tra di esse. Nella figura seguente viene illustrato uno scenario di questo tipo.  
  
 ![Schema logico per la dimensione di riferimento di esempio](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimindirect.gif "Schema logico per la dimensione di riferimento di esempio")  
  
 Nel diagramma precedente la tabella dei fatti **FactResellerSales** non dispone di una relazione di chiave esterna con la tabella delle dimensioni **DimGeography** . Tuttavia, la tabella dei fatti **FactResellerSales** ha una relazione di chiave esterna con la tabella delle dimensioni **DimReseller** , che a sua volta ha una relazione di chiave esterna con la tabella delle dimensioni **DimGeography** . Per definire una dimensione Reseller contenente le informazioni di geografia su ogni rivenditore, è necessario recuperare questi attributi dalle tabelle delle dimensioni **DimGeography** e **DimReseller** . In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tuttavia, è possibile ottenere lo stesso risultato creando due dimensioni separate e collegandole in un gruppo di misure definendo una relazione di tipo Riferimento tra le due dimensioni. Per ulteriori informazioni sulle relazioni tra le dimensioni di riferimento, vedere [relazioni tra dimensioni](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Un vantaggio dell'utilizzo di relazioni di tipo Riferimento in questo scenario consiste nella possibilità di creare un'unica dimensione Geography e quindi di creare più dimensioni del cubo basate sulla dimensione Geography, senza che sia necessario ulteriore spazio di archiviazione. È ad esempio possibile collegare una delle dimensioni Geography del cubo a una dimensione Reseller e un'altra delle dimensioni Geography del cubo a una dimensione Customer. **Argomenti correlati:** [Relazioni](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)tra le dimensioni, [definire una relazione di tipo riferimento e le proprietà delle relazioni a cui si fa riferimento](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>Elaborazione di una dimensione  
 Dopo avere creato una dimensione, per poter visualizzare i membri degli attributi e delle gerarchie della dimensione, è necessario elaborare la dimensione stessa. Dopo la modifica della struttura di una dimensione o l'aggiornamento delle informazioni nelle tabelle sottostanti, è necessario elaborare di nuovo la dimensione per poter visualizzare le modifiche. Quando si elabora una dimensione dopo modifiche strutturali, è inoltre necessario elaborare qualsiasi cubo in cui la dimensione è inclusa. In caso contrario, il cubo non sarà visualizzabile.  
  
## <a name="security"></a>Sicurezza  
 Tutti gli oggetti subordinati di una dimensione, inclusi membri, livelli e gerarchie, vengono protetti tramite ruoli in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La sicurezza delle dimensioni può essere applicata a tutti i cubi nel database che utilizzano la dimensione oppure a un solo cubo specifico. Per ulteriori informazioni sulla sicurezza delle dimensioni, vedere [concedere autorizzazioni per una &#40;dimensione&#41;Analysis Services](../multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Archiviazione dimensioni](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Traduzioni delle dimensioni](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Dimensioni abilitate per la scrittura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
