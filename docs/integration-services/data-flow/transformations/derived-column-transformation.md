---
description: Trasformazione Colonna derivata
title: Trasformazione Colonna derivata | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 93548684fb17ce59e5cee78e2a7a268dfce903ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430693"
---
# <a name="derived-column-transformation"></a>Trasformazione Colonna derivata

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
-   Specificare un'espressione per ogni colonna di input o nuova colonna da modificare. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Se un'espressione fa riferimento a una colonna di input sovrascritta dalla trasformazione Colonna derivata, l'espressione utilizzerà il valore originale della colonna anziché il valore derivato.  
  
-   Se si aggiungono i risultati a nuove colonne e il tipo di dati è **string**, specificare una tabella codici. Per altre informazioni, vedere [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 La trasformazione Colonna derivata condizionale include la proprietà personalizzata FriendlyExpression, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Usare le espressioni di proprietà nei pacchetti](../../../integration-services/expressions/use-property-expressions-in-packages.md)e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Questa trasformazione include un input, un output regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Derivazione di valori di colonna tramite la trasformazione Colonna derivata](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>Editor trasformazione Colonna derivata
  Usare la finestra di dialogo **Editor trasformazione Colonna derivata** per creare espressioni che popolino le colonne nuove o di sostituzione.  
  
### <a name="options"></a>Opzioni  
 **Variabili e Colonne**  
 Consente di compilare un'espressione che utilizza una variabile o una colonna di input tramite un'operazione di trascinamento della variabile o della colonna dall'elenco di variabili e colonne disponibili in una riga di tabella esistente nel riquadro sottostante o in una nuova riga alla fine dell'elenco.  
  
 **Funzioni e Operatori**  
 Compilare un'espressione che utilizza una funzione o un operatore per valutare i dati di input e indirizzare i dati di output trascinando le funzioni e gli operatori dall'elenco al riquadro sottostante.  
  
 **Nome colonna derivata**  
 Consente di assegnare un nome alla colonna derivata. L'impostazione predefinita è rappresentata da un elenco numerato di colonne derivate. È tuttavia possibile scegliere qualsiasi nome descrittivo e univoco.  
  
 **Colonna derivata**  
 Consente di selezionare una colonna derivata dall'elenco. Scegliere se aggiungere la colonna derivata come nuova colonna di output o sostituire i dati in una colonna esistente.  
  
 **Espressione**  
 Consente di digitare un'espressione o compilarne una mediante il trascinamento dal precedente elenco di colonne, variabili, funzioni e operatori disponibili.  
  
 È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.  
  
 **Argomenti correlati**: [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operatori &#40;espressione SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) e [Funzioni &#40;espressione SSIS&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **Tipo di dati**  
 Se si aggiungono dati a una nuova colonna, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene valutata automaticamente l'espressione e viene impostato automaticamente il tipo di dati appropriato. Il valore di questa colonna è di sola lettura. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Lunghezza**  
 Se si aggiungono dati a una nuova colonna, nella finestra di dialogo **Editor trasformazione colonna derivata** viene valutata automaticamente l'espressione e impostata la lunghezza della colonna per i dati stringa. Il valore di questa colonna è di sola lettura.  
  
 **Precisione**  
 Se si aggiungono dati a una nuova colonna, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene impostata automaticamente la precisione per i dati numerici in base al tipo di dati. Il valore di questa colonna è di sola lettura.  
  
 **Ridimensionamento**  
 Se si aggiungono dati a una nuova colonna, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene impostata automaticamente la scala per i dati numerici in base al tipo di dati. Il valore di questa colonna è di sola lettura.  
  
 **Tabella codici**  
 Se si aggiungono dati a una nuova colonna, nella finestra di dialogo **Editor trasformazione Colonna derivata** viene impostata automaticamente la tabella codici per il tipo di dati DT_STR. È possibile aggiornare **Tabella codici**.  
  
 **Configura output errori**  
 Consente di indicare come gestire gli errori tramite la finestra di dialogo [Configura output errori](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com  
