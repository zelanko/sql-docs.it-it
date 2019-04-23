---
title: Gestione degli errori e avvisi (XMLA) | Microsoft Docs
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
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156388"
---
# <a name="handling-errors-and-warnings-xmla"></a>Gestione di errori e avvisi (XMLA)
  Gestione degli errori è obbligatorio quando un file di XML for Analysis (XMLA) [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) oppure [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) chiamata al metodo non viene eseguito, viene eseguito correttamente, ma genera errori o avvisi, o viene eseguito correttamente ma restituisce risultati che contengono errori.  
  
|Errore|Report|  
|-----------|---------------|  
|Chiamata al metodo XMLA non eseguita|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Restituisce un messaggio di errore SOAP che contiene i dettagli dell'errore.<br /><br /> Per altre informazioni, vedere la sezione [la gestione degli errori SOAP](#handling_soap_faults).|  
|Errori o avvisi in una chiamata al metodo eseguita correttamente|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include un' [errore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) o [avviso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) (elemento) per ogni errore o avviso, rispettivamente, nelle [messaggi](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) proprietà del [radice](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento che contiene i risultati della chiamata al metodo.<br /><br /> Per altre informazioni, vedere la sezione [Handling Errors and Warnings](#handling_errors_and_warnings).|  
|Errori nel risultato di una chiamata al metodo eseguita correttamente|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include un inline `error` o `warning` (elemento) per l'errore o avviso, rispettivamente, all'interno di appropriato [cella](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) oppure [riga](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) elemento dei risultati della chiamata al metodo.<br /><br /> Per altre informazioni, vedere la sezione [la gestione degli errori e avvisi Inline](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a> Gestione di errori SOAP  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un errore SOAP quando si verificano le situazioni seguenti:  
  
-   Il messaggio SOAP che contiene il metodo XMLA non è in formato corretto o non è stato convalidato dall'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Si è verificato un errore di comunicazione o di altro tipo relativo al messaggio SOAP che contiene il metodo XMLA.  
  
-   Il metodo XMLA non è stato eseguito nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Il codice di errore SOAP per XMLstartA inizia con "XMLForAnalysis", seguito da un punto e dal codice esadecimale restituito HRESULT. Un codice di errore "`0x80000005`" viene formattato come "`XMLForAnalysis.0x80000005`". Per ulteriori informazioni sul formato degli errori SOAP, vedere l'argomento relativo nel documento Simple Object Access Protocol (SOAP) 1.1 del World Wide Web Consortium (W3C).  
  
### <a name="fault-code-information"></a>Informazioni sul codice di errore  
 Nella tabella seguente vengono elencate le informazioni sul codice di errore XMLA contenute nella sezione dei dettagli della risposta SOAP. Le colonne rappresentano gli attributi di un errore nella sezione dei dettagli di un errore SOAP.  
  
|Nome colonna|Tipo|Descrizione|Valore null consentito<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|Codice restituito che indica l'esito positivo o negativo del metodo. Il valore esadecimale deve essere convertito in un valore `UnsignedInt`.|No|  
|`WarningCode`|`UnsignedInt`|Codice restituito che indica una condizione di avviso. Il valore esadecimale deve essere convertito in un valore `UnsignedInt`.|Yes|  
|`Description`|`String`|Testo o descrizione dell'errore o dell'avviso restituiti dal componente che ha generato l'errore.|Yes|  
|`Source`|`String`|Nome del componente che ha generato l'errore o l'avviso.|Yes|  
|`HelpFile`|`String`|Percorso o URL del file o dell'argomento della Guida in cui è descritto l'errore o l'avviso.|Yes|  
  
 <sup>1</sup> indica se i dati sono obbligatorio e devono essere restituiti, o se i dati sono facoltativi e una stringa null è consentita se la colonna non è applicabile.  
  
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
  
##  <a name="handling_errors_and_warnings"></a> Gestione degli errori e avvisi  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene restituita la proprietà `Messages` nell'elemento `root` per un comando se si verificano le situazioni seguenti dopo l'esecuzione del comando:  
  
-   Il metodo non ha provocato alcun errore, ma si è verificato un errore nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dopo che la chiamata al metodo è stata eseguita correttamente.  
  
-   L'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un avviso quando il comando viene eseguito correttamente.  
  
 La proprietà `Messages` segue tutte le altre proprietà contenute nell'elemento `root` e può contenere uno o più elementi `Message`. A sua volta, ogni elemento `Message` può contenere un unico elemento `error` o `warning` che descrive rispettivamente tutti gli errori o gli avvisi che si sono verificati per il comando specificato.  
  
 Per altre informazioni sugli errori e avvisi che sono contenuti nel `Messages` proprietà, vedere [messaggi elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>Gestione di errori durante la serializzazione  
 Se si verifica un errore dopo il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza ha iniziato a serializzare l'output di un comando eseguito correttamente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un [eccezione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) elemento in uno spazio dei nomi diverso al momento dell'errore. L'istanza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] chiude quindi tutti gli elementi aperti in modo che il documento XML inviato al client sia un valido. L'istanza restituisce inoltre un elemento `Messages` che contiene la descrizione dell'errore.  
  
##  <a name="handling_inline_errors_and_warnings"></a> Gestione degli errori e avvisi Inline  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un elemento inline `error` o `warning` per un comando se il metodo XMLA non ha provocato alcun errore, ma si è verificato un errore specifico per un elemento dati nei risultati restituiti dal metodo nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dopo che la chiamata al metodo XMLA è stata eseguita in modo corretto.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce inline `error` e `warning` elementi se problemi specifici per una cella o altri dati che sono contenuti all'interno di un `root` elemento utilizzando la [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) tipo di dati vengono, ad esempio la sicurezza errore o la formattazione errore per una cella. In questi casi, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce un elemento `error` o `warning` nell'elemento `Cell` o `row` che contiene rispettivamente l'errore o l'avviso.  
  
 L'esempio seguente illustra un set di risultati che contiene un errore nel set di righe restituito da un' `Execute` metodo usando il [istruzione](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) comando.  
  
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
  
  
