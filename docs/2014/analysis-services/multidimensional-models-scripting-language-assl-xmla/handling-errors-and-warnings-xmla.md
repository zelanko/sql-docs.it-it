---
title: Gestione di errori e avvisi (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702128"
---
# <a name="handling-errors-and-warnings-xmla"></a>Gestione di errori e avvisi (XMLA)
  La gestione degli errori è obbligatoria quando una chiamata al metodo [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) di XML for Analysis (XMLA) non viene eseguita, viene eseguita correttamente, ma genera errori o avvisi oppure viene eseguita correttamente, ma restituisce risultati che contengono errori.  
  
|Errore|Creazione di report|  
|-----------|---------------|  
|Chiamata al metodo XMLA non eseguita|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un messaggio di errore SOAP contenente i dettagli dell' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] errore.<br /><br /> Per ulteriori informazioni, vedere la sezione relativa alla [gestione degli errori SOAP](#handling_soap_faults).|  
|Errori o avvisi in una chiamata al metodo eseguita correttamente|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]include un elemento [Error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) o [warning](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) per ogni errore o avviso, rispettivamente, nella proprietà [messages](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) dell'elemento [radice](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) che contiene i risultati della chiamata al metodo.<br /><br /> Per ulteriori informazioni, vedere la sezione [gestione di errori e avvisi](#handling_errors_and_warnings).|  
|Errori nel risultato di una chiamata al metodo eseguita correttamente|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]include un elemento `error` inline `warning` o per l'errore o l'avviso, rispettivamente, all'interno dell'elemento [Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) o [Row](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) appropriato dei risultati della chiamata al metodo.<br /><br /> Per ulteriori informazioni, vedere la sezione [gestione di errori e avvisi inline](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a>Gestione degli errori SOAP  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un errore SOAP quando si verificano le situazioni seguenti:  
  
-   Il messaggio SOAP che contiene il metodo XMLA non è in formato corretto o non è stato convalidato dall'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Si è verificato un errore di comunicazione o di altro tipo relativo al messaggio SOAP che contiene il metodo XMLA.  
  
-   Il metodo XMLA non è stato eseguito nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Il codice di errore SOAP per XMLstartA inizia con "XMLForAnalysis", seguito da un punto e dal codice esadecimale restituito HRESULT. Un codice di errore "`0x80000005`" viene formattato come "`XMLForAnalysis.0x80000005`". Per ulteriori informazioni sul formato degli errori SOAP, vedere l'argomento relativo nel documento Simple Object Access Protocol (SOAP) 1.1 del World Wide Web Consortium (W3C).  
  
### <a name="fault-code-information"></a>Informazioni sul codice di errore  
 Nella tabella seguente vengono elencate le informazioni sul codice di errore XMLA contenute nella sezione dei dettagli della risposta SOAP. Le colonne rappresentano gli attributi di un errore nella sezione dei dettagli di un errore SOAP.  
  
|Nome colonna|Type|Descrizione|Valore null consentito<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|Codice restituito che indica l'esito positivo o negativo del metodo. Il valore esadecimale deve essere convertito in un valore `UnsignedInt`.|No|  
|`WarningCode`|`UnsignedInt`|Codice restituito che indica una condizione di avviso. Il valore esadecimale deve essere convertito in un valore `UnsignedInt`.|Sì|  
|`Description`|`String`|Testo o descrizione dell'errore o dell'avviso restituiti dal componente che ha generato l'errore.|Sì|  
|`Source`|`String`|Nome del componente che ha generato l'errore o l'avviso.|Sì|  
|`HelpFile`|`String`|Percorso o URL del file o dell'argomento della Guida in cui è descritto l'errore o l'avviso.|Sì|  
  
 <sup>1</sup> indica se i dati sono obbligatori e devono essere restituiti o se i dati sono facoltativi ed è consentita una stringa null se la colonna non è applicabile.  
  
 Di seguito viene riportato un esempio di errore SOAP che si è verificato quando una chiamata al metodo non è riuscita:  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a>Gestione di errori e avvisi  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene restituita la proprietà `Messages` nell'elemento `root` per un comando se si verificano le situazioni seguenti dopo l'esecuzione del comando:  
  
-   Il metodo non ha provocato alcun errore, ma si è verificato un errore nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dopo che la chiamata al metodo è stata eseguita correttamente.  
  
-   L'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un avviso quando il comando viene eseguito correttamente.  
  
 La proprietà `Messages` segue tutte le altre proprietà contenute nell'elemento `root` e può contenere uno o più elementi `Message`. A sua volta, ogni elemento `Message` può contenere un unico elemento `error` o `warning` che descrive rispettivamente tutti gli errori o gli avvisi che si sono verificati per il comando specificato.  
  
 Per ulteriori informazioni sugli errori e sugli avvisi contenuti nella `Messages` proprietà, vedere [elementi messages &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>Gestione di errori durante la serializzazione  
 Se si verifica un errore dopo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che l'istanza ha già iniziato a serializzare l'output di un comando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eseguito correttamente, restituisce un elemento [Exception](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) in uno spazio dei nomi diverso al momento dell'errore. L'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] chiude quindi tutti gli elementi aperti in modo che il documento XML inviato al client sia un valido. L'istanza restituisce inoltre un elemento `Messages` che contiene la descrizione dell'errore.  
  
##  <a name="handling_inline_errors_and_warnings"></a>Gestione di errori e avvisi inline  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un elemento inline `error` o `warning` per un comando se il metodo XMLA non ha provocato alcun errore, ma si è verificato un errore specifico per un elemento dati nei risultati restituiti dal metodo nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dopo che la chiamata al metodo XMLA è stata eseguita in modo corretto.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fornisce `error` elementi inline `warning` e se si verificano problemi specifici di una cella o di altri dati contenuti all' `root` interno di un elemento utilizzando il tipo di dati [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) , ad esempio un errore di sicurezza o un errore di formattazione per una cella. In questi casi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un elemento `error` o `warning` nell'elemento `Cell` o `row` che contiene rispettivamente l'errore o l'avviso.  
  
 Nell'esempio seguente viene illustrato un set di risultati contenente un errore nel set di righe restituito da `Execute` un metodo utilizzando il comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) .  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
