---
title: Usare la modalità PATH con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode
- characters [SQL Server], XML
- aliases [SQL Server], XML
- FOR XML clause, PATH mode
- FOR XML PATH mode
- column names [SQL Server]
- XPath queries [SQL Server]
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 874c410e389282aa4cfcdbc002e941ca44c413df
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702357"
---
# <a name="use-path-mode-with-for-xml"></a>Utilizzare la modalità PATH con FOR XML
  Come descritto nell'argomento [Costruzione di codice XML tramite la clausola FOR XML](for-xml-sql-server.md), la modalità PATH consente di combinare in modo più semplice elementi e attributi. e di introdurre nidificazione aggiuntiva per la rappresentazione di proprietà complesse. È possibile utilizzare query in modalità FOR XML EXPLICIT per la costruzione di questo tipo di strutture XML da un set di righe, ma la modalità PATH costituisce un'alternativa più semplice alla formulazione di query in modalità EXPLICIT, che può essere un'operazione complessa. La modalità PATH, insieme alla possibilità di scrivere query FOR XML nidificate e alla direttiva TYPE per restituire istanze di tipo **xml** , consente di formulare più facilmente le query.  
  
 In modalità PATH i nomi e gli alias di colonna vengono gestiti come espressioni XPath. Queste espressioni indicano il modo in cui viene eseguito il mapping tra i valori e il codice XML. Ogni espressione XPath è un XPath relativo che specifica il tipo dell'elemento, ad esempio attributo, elemento e valore scalare, nonché il nome e la gerarchia del nodo che verrà generato in relazione all'elemento riga.  
  
 In questa sezione viene descritto il mapping delle colonne in un set di righe in varie condizioni e vengono forniti alcuni esempi.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Colonne senza nome](columns-without-a-name.md)  
  
-   [Colonne provviste di un nome](columns-with-a-name.md)  
  
-   [Colonne con nome specificato come carattere jolly](columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [Colonne con il nome di un test di nodo XPath](columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [Nomi di colonna con il percorso specificato come data&#40;&#41;](column-names-with-the-path-specified-as-data.md)  
  
-   [Colonne contenenti un valore NULL per impostazione predefinita](columns-that-contain-a-null-value-by-default.md)  
  
-   [Supporto dello spazio dei nomi in modalità di PATH](namespace-support-in-path-mode.md)  
  
-   [Esempi d'uso della modalità PATH](examples-using-path-mode.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
