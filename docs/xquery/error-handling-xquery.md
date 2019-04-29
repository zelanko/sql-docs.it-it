---
title: Gestione degli errori (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 78a89ddcb27111396ec279af0b418e8490780e6a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934595"
---
# <a name="error-handling-xquery"></a>Gestione degli errori (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  La specifica W3C consente la generazione di errori statica oppure dinamica e definisce gli errori statici, dinamici e di tipo.  
  
## <a name="compilation-and-error-handling"></a>Compilazione e gestione degli errori  
 Gli errori di compilazione derivano da espressioni XQuery e istruzioni XML DML con sintassi non corretta. Durante la fase di compilazione viene verificata la correttezza dei tipi statici di espressioni XQuery e istruzioni DML e vengono utilizzati XML Schema per l'inferenza dei tipi per gli XML tipizzati. Viene generato un errore di tipo statico se è possibile che, in fase di esecuzione, un'espressione non riesca a causa di una violazione dell'indipendenza dai tipi. Questo si verifica ad esempio quando una stringa viene sommata a un valore intero oppure si esegue una query per individuare dati tipizzati in un nodo inesistente.  
  
 Diversamente da quanto previsto dallo standard W3C, gli errori di run-time di XQuery vengono convertiti in sequenze vuote, che possono essere propagate come valori vuoti XML o NULL al risultato della query, a seconda del contesto di chiamata.  
  
 Per evitare gli errori statici è possibile eseguire il cast esplicito al tipo corretto, tuttavia gli errori di cast che si verificano in fase di esecuzione vengono convertiti in sequenze vuote.  
  
## <a name="static-errors"></a>Errori statici  
 Gli errori statici vengono restituiti utilizzando il meccanismo di gestione degli errori [!INCLUDE[tsql](../includes/tsql-md.md)]. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], gli errori di tipo XQuery vengono restituiti in modo statico. Per altre informazioni, vedere [XQuery e tipizzazione statica](../xquery/xquery-and-static-typing.md).  
  
## <a name="dynamic-errors"></a>Errori dinamici  
 In XQuery, nella maggior parte dei casi sugli errori dinamici viene eseguito il mapping a una sequenza vuota ("()"), Tuttavia, queste sono le due eccezioni: Condizioni di overflow nelle funzioni di aggregazione XQuery ed errori di convalida XML DML. Si noti che nella maggior parte dei casi sugli errori dinamici viene eseguito il mapping a una sequenza vuota ("()"). In caso contrario, l'esecuzione della query che utilizza gli indici XML può generare errori imprevisti. Pertanto, per garantire un'esecuzione efficiente senza la generazione di errori imprevisti, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] esegue il mapping degli errori dinamici a ().  
  
 Nei casi in cui l'errore dinamico verrebbe generato all'interno di un predicato, spesso non generare l'errore non modifica la semantica, poiché () viene eseguito il mapping a False. In alcuni casi tuttavia, la restituzione di () invece di un errore dinamico può causare risultati imprevisti, come illustrato negli esempi seguenti.  
  
### <a name="example-using-the-avg-function-with-a-string"></a>Esempio: Utilizzo della funzione AVG () con una stringa  
 Nell'esempio seguente, il [AVG-funzione](../xquery/aggregate-functions-avg.md) viene chiamato per calcolare la media dei tre valori. Uno dei valori è una stringa. Poiché l'istanza XML in questo caso è non tipizzata, tutti i dati al suo interno sono di tipo atomico non tipizzato. Il **AVG ()** funzione prima di tutto viene eseguito il cast questi valori per **xs: double** prima di calcolare la Media. Tuttavia, il valore `"Hello"`, non è possibile eseguire il cast **xs: double** e crea un errore dinamico. In questo caso, invece di restituire un errore dinamico, il cast di `"Hello"` al **xs: double** genera una sequenza vuota. Il **AVG ()** funzione ignora questo valore, calcola la media degli altri due valori e restituisce 150.  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>Esempio: Utilizzando not (funzione)  
 Quando si usa la [non funzionerà](../xquery/functions-on-boolean-values-not-function.md) in un predicato, ad esempio, `/SomeNode[not(Expression)]`, e l'espressione genera un errore dinamico, è verrà restituita una sequenza vuota anziché un errore. Applicando **NOT ()** alla sequenza vuota restituisce True, anziché un errore.  
  
### <a name="example-casting-a-string"></a>Esempio: Cast di una stringa  
 Nell'esempio seguente viene eseguito il cast della stringa letterale "NaN" a xs:string, quindi a xs:double. Il risultato è un set di righe vuoto. Anche se non è possibile eseguire correttamente il cast della stringa "NaN" a xs:double, questo fatto non può essere determinato fino al momento dell'esecuzione, perché prima viene eseguito il cast della stringa a xs:string.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 In questo esempio tuttavia, viene generato un errore di tipo statico.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Il **fn:error()** funzione non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Nozioni fondamentali su XQuery](../xquery/xquery-basics.md)  
  
  
