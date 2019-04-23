---
title: Convenzioni XML di ASSL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41e0a3fcf4348efcb2108a1205c1d2d8eabfb85c
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156689"
---
# <a name="assl-xml-conventions"></a>Convenzioni XML di ASSL
  Nel linguaggio ASSL (Analysis Services Scripting Language) la gerarchia di oggetti viene rappresentata come un set di tipi di elementi, ciascuno dei quali definisce gli elementi figlio che può contenere.  
  
 Per rappresentare la gerarchia di oggetti, in ASSL vengono utilizzate le convenzioni XML seguenti:  
  
-   Tutti gli oggetti e proprietà sono rappresentate come elementi, ad eccezione degli attributi XML standard, ad esempio "XML: lang".  
  
-   Sia i nomi degli elementi e i valori di enumerazione seguono la convenzione di denominazione di Microsoft .NET Framework della convenzione Pascal maiuscole e minuscole senza caratteri di sottolineatura.  
  
-   La combinazione di lettere maiuscole e minuscole di tutti i valori viene mantenuta. I valori relativi alle enumerazioni rispettano inoltre la distinzione tra maiuscole e minuscole.  
  
 Oltre all'elenco di convenzioni indicato, in Analysis Services vengono seguite inoltre convenzioni specifiche relative alla cardinalità, l'ereditarietà, gli spazi vuoti, i tipi di dati e i valori predefiniti.  
  
## <a name="cardinality"></a>Cardinalità  
 Quando la cardinalità di un elemento è maggiore di 1, è presente una raccolta di elementi XML che incapsula tale elemento. Per il nome della raccolta viene utilizzata la forma plurale degli elementi contenuti nella raccolta stessa. Nel frammento XML seguente, ad esempio, viene rappresentata la raccolta `Dimensions` in un elemento `Database`:  
  
 `<Database>`  
  
 `...`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 L'ordine in cui sono visualizzati gli elementi non è importante.  
  
## <a name="inheritance"></a>Ereditarietà  
 L'ereditarietà viene utilizzata quando sono presenti oggetti distinti cui sono associati set di proprietà sovrapposti, ma con differenze significative. Esempi di tali oggetti sovrapposti, ma distinti, sono i cubi virtuali, i cubi collegati e i cubi regolari. Per questo tipo di oggetti, in Analysis Services viene utilizzato l'attributo standard `type` dello spazio dei nomi di istanze XML per indicare l'ereditarietà. Nel frammento XML seguente viene illustrato ad esempio il modo in cui l'attributo `type` identifica se un elemento `Cube` eredita da un cubo regolare o da un cubo virtuale:  
  
 `<Cubes>`  
  
 `<Cube xsi:type="RegularCube">`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type="VirtualCube">`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 In genere l'ereditarietà non viene utilizzata quando a più tipi è associata una proprietà con lo stesso nome. Le proprietà `Name` e `ID` vengono visualizzate ad esempio in molti elementi, ma non sono state promosse a un tipo astratto.  
  
## <a name="whitespace"></a>Spazi vuoti  
 Gli spazi vuoti all'interno di un valore di elemento vengono mantenuti, mentre gli spazi vuoti iniziali e finali vengono sempre rimossi. Gli elementi seguenti contengono ad esempio lo stesso testo che differisce tuttavia per il numero di spazi vuoti all'interno. Di conseguenza tali elementi vengono considerati come se i relativi valori fossero diversi:  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 Gli elementi seguenti differiscono invece solo per gli spazi vuoti iniziali e finali e vengono pertanto considerati come se i relativi valori fossero equivalenti:  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>Tipi di dati  
 In Analysis Services vengono utilizzati i seguenti tipi di dati XML Schema Definition Language (XSD) standard:  
  
 `Int`  
 Valore intero compreso nell'intervallo tra-231-1 231.  
  
 `Long`  
 Valore intero nell'intervallo di -263 e 263-1.  
  
 `String`  
 Valore stringa conforme alle regole globali seguenti:  
  
-   Rimozione dei caratteri di controllo.  
  
-   Eliminazione degli spazi vuoti iniziali e finali.  
  
-   Mantenimento degli spazi vuoti interni.  
  
 Per le proprietà `Name` e `ID` sono presenti limitazioni speciali relative ai caratteri validi negli elementi della stringa. Per ulteriori informazioni sul `Name` e `ID` convenzioni, vedere [oggetti ASSL e relative caratteristiche](assl-objects-and-object-characteristics.md).  
  
 `DateTime`  
 Oggetto `DateTime` struttura da .NET Framework. Un valore `DateTime` non può essere NULL. La data meno recente supportata dal tipo di dati `DataTime` è rappresentata dall'1 gennaio 1601, disponibile per i programmatori come `DateTime.MinValue`. La data meno recente supportata indica che un valore `DateTime` è mancante.  
  
 `Boolean`  
 Enumerazione con due soli valori, ovvero {true, false} o {0, 1}.  
  
## <a name="default-values"></a>Valori predefiniti  
 In Analysis Services vengono utilizzati i valori predefiniti elencati nella tabella seguente.  
  
|Tipo di dati XML|Valore predefinito|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|"" (stringa vuota)|  
|`Integer` o `Long`|0 (zero)|  
|`Timestamp`|12:00:00 AM, 1/1/0001 (corrispondente a una le versioni di .NET Framework `System.DateTime` con 0 tick)|  
  
 Un elemento presente, ma vuoto, viene interpretato come se il relativo valore fosse una stringa Null e non quello predefinito.  
  
### <a name="inherited-defaults"></a>Valori predefiniti ereditati  
 Alcune proprietà specificate per un oggetto forniscono i valori predefiniti per la stessa proprietà in oggetti figlio o discendenti. `Cube.StorageMode` fornisce ad esempio il valore predefinito per `Partition.StorageMode`. Le regole che Analysis Services applica ai valori predefiniti ereditati sono i seguenti:  
  
-   Quando in XML la proprietà per l'oggetto figlio è Null, per impostazione predefinita viene utilizzato il valore ereditato. Se tuttavia si esegue una query relativa al valore nel server, viene restituito il valore Null dell'elemento XML.  
  
-   Non è possibile determinare a livello di programmazione se la proprietà di un oggetto figlio è stata impostata direttamente su tale oggetto oppure se è stata ereditata.  
  
 Per alcuni elementi sono specificati valori predefiniti che si applicano quando l'elemento è mancante. Gli elementi `Dimension` nel frammento XML seguente, ad esempio, sono equivalenti anche se un elemento `Dimension` contiene un elemento `Visible`, mentre l'altro elemento `Dimension` non lo contiene.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Per altre informazioni sui valori predefiniti ereditati, vedere [oggetti ASSL e relative caratteristiche](assl-objects-and-object-characteristics.md).  
  
  
