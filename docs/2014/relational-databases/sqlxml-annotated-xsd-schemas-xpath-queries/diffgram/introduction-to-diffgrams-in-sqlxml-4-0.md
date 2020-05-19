---
title: Introduzione a DiffGram in SQLXML 4,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2de8eaa81c5a2e903be2f9bd608c6ccca703718d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703138"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>Introduzione ai DiffGram in SQLXML 4.0
  In questo argomento viene fornita una breve introduzione ai DiffGram.  
  
## <a name="diffgram-format"></a>Formato DiffGram  
 Il formato DiffGram generale è il seguente:  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 Il formato DiffGram è costituito dai blocchi seguenti:  
  
 **\<>DataInstance**  
 Il nome di questo elemento, **DataInstance**, viene usato a scopo di spiegazione in questa documentazione. Se, ad esempio, il DiffGram è stato generato da un set di dati nel .NET Framework, il valore della proprietà **Name** del set di dati verrebbe utilizzato come nome di questo elemento. Questo blocco contiene tutti i dati rilevanti dopo la modifica, inclusi eventualmente i dati che non sono stati modificati. La logica di elaborazione DiffGram ignora gli elementi in questo blocco per i quali non è specificato l'attributo **diffgr: hasChanges** .  
  
 **\<diffgr: prima di>**  
 Questo blocco facoltativo contiene le istanze dei record originali (elementi) che devono essere aggiornate o eliminate. Tutte le tabelle di database modificate (aggiornate o eliminate) dal DiffGram devono essere visualizzate come elementi di primo livello nel blocco ** \< before>** .  
  
 **\<diffgr: errori>**  
 Questo blocco facoltativo viene ignorato dalla logica di elaborazione DiffGram.  
  
## <a name="diffgram-annotations"></a>Annotazioni DiffGram  
 Queste annotazioni sono definite nello spazio dei nomi DiffGram **"urn: schemas-microsoft-com: XML-DiffGram-01"**:  
  
 **id**  
 Questo attributo viene utilizzato per associare gli elementi in ** \< prima di>** e i blocchi di ** \<>DataInstance** .  
  
 **hasChanges**  
 Per un'operazione di inserimento o aggiornamento, il DiffGram deve specificare questo attributo con il valore **inserito** o **modificato**. Se questo attributo non è presente, l'elemento corrispondente nel ** \<>DataInstance** viene ignorato dalla logica di elaborazione e non vengono eseguiti aggiornamenti. Per esempi funzionanti, vedere [esempi di DiffGram &#40;SQLXML 4,0&#41;](diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 Questo attributo viene utilizzato per specificare relazioni padre-figlio tra gli elementi nel DiffGram. Questo attributo viene visualizzato solo nel \< blocco before>. e viene utilizzato da SQLXML durante l'applicazione di aggiornamenti. La relazione padre-figlio viene utilizzata per determinare l'ordine in cui gli elementi vengono elaborati nel DiffGram.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>Informazioni sulla logica di elaborazione DiffGram  
 La logica di elaborazione DiffGram utilizza determinate regole per stabilire se un'operazione è di inserimento, aggiornamento o eliminazione. Tali regole sono descritte nella tabella seguente:  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|Insert|Un DiffGram indica un'operazione di inserimento quando un elemento viene visualizzato nel blocco ** \<>DataInstance** ma non nel blocco ** \< precedente>** corrispondente e l'attributo **diffgr: hasChanges** viene specificato (**diffgr: hasChanges = inserted**) nell'elemento. In questo caso, il DiffGram inserisce nel database l'istanza del record specificata nel blocco ** \<>DataInstance** .<br /><br /> Se l'attributo **diffgr: hasChanges** non è specificato, l'elemento viene ignorato dalla logica di elaborazione e non viene eseguita alcuna operazione di inserimento. Per esempi funzionanti, vedere [esempi di DiffGram &#40;SQLXML 4,0&#41;](diffgram-examples-sqlxml-4-0.md).|  
|Aggiornamento|Il DiffGram indica un'operazione di aggiornamento quando è presente un elemento nel blocco \< before> per il quale è presente un elemento corrispondente nel blocco ** \< DataInstance>** (ovvero, entrambi gli elementi hanno un attributo **diffgr: ID** con lo stesso valore) e l'attributo **diffgr: hasChanges** viene specificato con il valore **modificato** nell'elemento nel blocco di ** \<>DataInstance** .<br /><br /> Se l'attributo **diffgr: hasChanges** non è specificato nell'elemento nel blocco ** \<>DataInstance** , viene restituito un errore dalla logica di elaborazione. Per esempi funzionanti, vedere [esempi di DiffGram &#40;SQLXML 4,0&#41;](diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** viene specificato nel blocco ** \< before>** , viene utilizzata la relazione padre-figlio degli elementi specificati da **parentID** per determinare l'ordine in cui vengono aggiornati i record.|  
|Elimina|Un DiffGram indica un'operazione di eliminazione quando un elemento viene visualizzato nel blocco ** \< before>** ma non nel blocco ** \<>DataInstance** corrispondente. In questo caso, il DiffGram elimina l'istanza del record specificata nel blocco ** \< before>** dal database. Per esempi funzionanti, vedere [esempi di DiffGram &#40;SQLXML 4,0&#41;](diffgram-examples-sqlxml-4-0.md).<br /><br /> Se **diffgr: parentID** viene specificato nel blocco ** \< before>** , viene utilizzata la relazione padre-figlio degli elementi specificati da **parentID** per determinare l'ordine in cui vengono eliminati i record.|  
  
> [!NOTE]  
>  Non è possibile passare parametri ai DiffGram.  
  
  
