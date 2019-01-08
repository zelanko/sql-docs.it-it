---
title: Trasformazione Colonna derivata | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntrans.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5575991201f48c48fee1b27ad95b6d07de6251ba
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373893"
---
# <a name="derived-column-transformation"></a>Trasformazione Colonna derivata
  La trasformazione Colonna derivata consente di creare nuovi valori di colonna tramite l'applicazione di espressioni alle colonne di input della trasformazione. Un'espressione può contenere qualsiasi combinazione di variabili, funzioni, operatori e colonne dell'input della trasformazione. Il risultato può essere aggiunto come nuova colonna o inserito in una colonna esistente come valore di sostituzione. La trasformazione Colonna derivata può definire più colonne derivate e qualsiasi variabile o colonna di input può comparire in più espressioni.  
  
 È possibile utilizzare questa trasformazione per eseguire le attività seguenti:  
  
-   Concatenare i dati di colonne diverse in una colonna derivata. È ad esempio possibile combinare i valori delle colonne **FirstName** e **LastName** in una singola colonna derivata di nome **FullName**, usando l'espressione `FirstName + " " + LastName`.  
  
-   Estrarre caratteri da dati stringa, tramite funzioni quali SUBSTRING, e quindi archiviare il risultato in una colonna derivata. È ad esempio possibile estrarre l'iniziale del nome di una persona dalla colonna **FirstName** usando l'espressione `SUBSTRING(FirstName,1,1)`.  
  
-   Applicare funzioni matematiche a dati numerici e archiviare i risultati in una colonna derivata. È ad esempio possibile modificare la lunghezza e la precisione della colonna numerica **SalesTax**impostandola su un numero con due cifre decimali, usando l'espressione `ROUND(SalesTax, 2)`.  
  
-   Creare espressioni che confrontano colonne di input e variabili. È ad esempio possibile usare l'espressione **per confrontare la variabile** Version **con i dati nella colonna**ProductVersion **e, a seconda del risultato del confronto, usare il valore di** Version **o**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Estrarre parti di un valore datetime. È ad esempio possibile usare le funzioni GETDATE e DATEPART per estrarre l'anno corrente usando l'espressione `DATEPART("year",GETDATE())`.  
  
-   Consente di convertire le stringhe di data in un formato specifico usando un'espressione.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Configurazione della trasformazione Colonna derivata  
 Per configurare la trasformazione Colonna derivata, procedere nel modo seguente:  
  
-   Specificare un'espressione per ogni colonna di input o nuova colonna da modificare. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Se un'espressione fa riferimento a una colonna di input sovrascritta dalla trasformazione Colonna derivata, l'espressione utilizzerà il valore originale della colonna anziché il valore derivato.  
  
-   Se si aggiungono i risultati a nuove colonne e il tipo di dati è `string`, specificare una tabella codici. Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).  
  
 La trasformazione Colonna derivata condizionale include la proprietà personalizzata FriendlyExpression, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Usare le espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md)e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input, un output regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Colonna derivata** , vedere [Editor trasformazione Colonna derivata](../../derived-column-transformation-editor.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostare le proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Derivare i valori di colonna tramite la trasformazione Colonna derivata](derived-column-transformation.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com  
  
 Risposta curata [How to Split Column Data using SSIS](https://go.microsoft.com/fwlink/?LinkId=321995)(Come suddividere i dati delle colonne mediante SSIS) su curatedviews.cloudapp.net.  
  
  
