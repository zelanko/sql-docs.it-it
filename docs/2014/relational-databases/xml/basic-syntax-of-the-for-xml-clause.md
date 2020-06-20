---
title: Sintassi di base della clausola FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: rothja
ms.author: jroth
ms.openlocfilehash: dc0410e7a54674673f64442d8a3cf9476d250033
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059561"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>Sintassi di base della clausola FOR XML
  La modalità FOR XML può essere RAW, AUTO, EXPLICIT o PATH. Tale modalità determina la forma della struttura XML risultante.  
  
> [!IMPORTANT]  
>  La direttiva XMLDATA all'opzione FOR XML è deprecata. Utilizzare la generazione XSD in caso di modalità RAW e AUTO. Non sono disponibili sostituzioni per la direttiva XMLDATA in modalità EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Di seguito viene indicata la sintassi di base descritta nell'argomento [Clausola FOR (Transact-SQL)](/sql/t-sql/queries/select-for-clause-transact-sql):  
  
```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]   
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  
  
## <a name="arguments"></a>Argomenti  
 RAW[('*ElementName*')]  
 Accetta il risultato della query e trasforma ogni riga del set di risultati in un elemento XML con un identificatore generico, \<row /> , come tag dell'elemento. È possibile specificare facoltativamente il nome dell'elemento riga quando si utilizza questa direttiva. La struttura XML risultante utilizzerà il valore *ElementName* specificato come elemento riga generato per ogni riga. Per altre informazioni, vedere [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 AUTO  
 Restituisce i risultati della query in un semplice albero XML nidificato. Ogni tabella nella clausola FROM, per cui è specificata almeno una colonna nella clausola SELECT, viene rappresentata come elemento XML. Le colonne elencate nella clausola SELECT vengono mappate agli attributi di elemento appropriati. Per altre informazioni, vedere [Usare la modalità AUTO con FOR XML](use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Specifica che la forma dell'albero XML risultante viene definita in modo esplicito. Con questa modalità è tuttavia necessario che le query siano scritte in modo che le informazioni aggiuntive sulla nidificazione desiderata vengano specificate in modo esplicito. Per altre informazioni, vedere [Usare la modalità EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md).  
  
 PATH  
 Consente di combinare facilmente elementi e attributi, nonché di introdurre una nidificazione aggiuntiva per rappresentare proprietà complesse. È possibile utilizzare le query in modalità FOR XML EXPLICIT per costruire questo tipo di struttura XML da un set di righe, ma la modalità PATH costituisce un'alternativa più semplice. La modalità PATH, insieme alla possibilità di scrivere query FOR XML nidificate e alla direttiva TYPE per restituire istanze di tipo **xml** , consente di formulare più facilmente le query. e rappresenta un'alternativa alla scrittura della maggior parte delle query in modalità EXPLICIT. Per impostazione predefinita, la modalità PATH genera un \<row> wrapper di elemento per ogni riga del set di risultati. È possibile specificare facoltativamente il nome di un elemento. In tal caso, il nome specificato viene utilizzato come nome dell'elemento wrapper. Se si specifica una stringa vuota (FOR XML PATH ('')), non viene generato alcun elemento wrapper. Per altre informazioni, vedere [Usare la modalità PATH con FOR XML](use-path-mode-with-for-xml.md).  
  
 XMLDATA  
 Specifica che deve essere restituito uno schema XDR (XML-Data Reduced) inline. Lo schema viene aggiunto all'inizio del documento come schema inline. Per un esempio funzionante, vedere [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 XMLSCHEMA  
 Restituisce XML Schema W3C (XSD) inline. È possibile specificare facoltativamente un URI dello spazio dei nomi di destinazione quando si specifica questa direttiva. In tal modo, viene restituito lo spazio dei nomi specificato nello schema. Per altre informazioni, vedere [Generare uno schema XSD inline](generate-an-inline-xsd-schema.md). Per un esempio funzionante, vedere [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 ELEMENTS  
 Se si specifica l'opzione ELEMENTS, le colonne vengono restituite come sottoelementi. In caso contrario, vengono mappate ad attributi XML. Questa opzione è supportata solo con le modalità RAW, AUTO e PATH. È possibile specificare facoltativamente XSINIL o ABSENT quando si utilizza questa direttiva. XSINIL specifica la creazione di un elemento con attributo **xsi:nil** impostato su True per i valori di colonna NULL. Per impostazione predefinita o quando si specifica ABSENT insieme a ELEMENTS, non viene creato alcun elemento per i valori NULL. Per un esempio funzionante, vedere [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md) e [Usare la modalità AUTO con FOR XML](use-auto-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Se si specifica l'opzione BINARY Base64, gli eventuali dati binari restituiti dalla query vengono rappresentanti nel formato con codifica Base64. Per recuperare dati binari in modalità RAW ed EXPLICIT, è necessario specificare questa opzione. In modalità AUTO, i dati binari vengono restituiti come riferimento per impostazione predefinita. Per un esempio funzionante, vedere [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 TYPE  
 Specifica che la query restituisce i risultati come dati di tipo **xml** . Per altre informazioni, vedere [Direttiva TYPE nelle query FOR XML](type-directive-in-for-xml-queries.md).  
  
 ROOT [('*RootName*')]  
 Specifica l'aggiunta di un singolo elemento principale alla struttura XML risultante. È possibile specificare facoltativamente il nome dell'elemento radice da generare. Il valore predefinito è "root".  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)   
 [Usare la modalità AUTO con FOR XML](use-auto-mode-with-for-xml.md)   
 [Usare la modalità EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)   
 [Usare la modalità PATH con FOR XML](use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
