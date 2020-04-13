---
title: Generazione di XML da set di righe con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, generating XML from rowsets
ms.assetid: d061c0f1-3de9-4ad1-bbca-ce45d064b6c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93534392fd8d79ca71064bb0df61be7533dd6e06
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665282"
---
# <a name="generate-xml-from-rowsets-with-for-xml"></a>Generazione di XML da set di righe con FOR XML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile generare un'istanza del tipo di dati **xml** da un set di righe utilizzando FOR XML con la nuova direttiva **TYPE** .  
  
 Il risultato può essere assegnato a una colonna, a una variabile o a un parametro con tipo di dati **xml** . L'istruzione FOR XML può essere inoltre nidificata, consentendo di creare qualsiasi tipo di struttura gerarchica. Le istruzioni FOR XML nidificate sono molto più facili da scrivere rispetto a FOR XML EXPLICIT, ma forniscono prestazioni inferiori in caso di gerarchie con numerosi livelli. L'istruzione FOR XML introduce inoltre una nuova modalità PATH, che specifica il percorso dell'albero XML in cui compare un determinato valore di colonna.  
  
 La nuova direttiva **FOR XML TYPE** consente di definire visualizzazioni XML in sola lettura su dati relazionali con la sintassi SQL. Su tale vista è possibile eseguire query utilizzando istruzioni SQL e istruzioni XQuery incorporate, come illustrato nell'esempio seguente. È possibile fare riferimento a tali viste SQL anche nelle stored procedure.  
  
## <a name="example-sql-view-returning-generated-xml-data-type"></a>Esempio: visualizzazione SQL che restituisce un tipo di dati xml generato  
 La definizione di vista SQL seguente crea una visualizzazione XML su una colonna relazionale, utilizzando la chiave primaria e gli autori dei libri recuperati da una colonna XML:  
  
```  
CREATE VIEW V (xmlVal) AS  
SELECT pk, xCol.query('/book/author')  
FROM   T  
FOR XML AUTO, TYPE  
```  
  
 La vista V contiene una singola riga con una singola colonna con nome xmlVal e tipo XML`.` Può essere utilizzata nelle query come una normale istanza del tipo di dati **xml** . La query seguente, ad esempio, restituisce il nome dell'autore, "David":  
  
```  
SELECT xmlVal.query('//author[first-name = "David"]')  
FROM   V  
```  
  
 Le definizioni delle viste SQL sono analoghe alle visualizzazioni XML create utilizzando schemi con annotazioni, ma esistono alcune differenze importanti. La definizione della vista SQL è in modalità di sola lettura e deve essere modificata tramite istruzioni XQuery incorporate. Le viste XML vengono create utilizzando schemi con annotazioni. Inoltre, in una vista SQL il risultato XML viene materializzato prima di applicare l'espressione XQuery, mentre le query XPath sulle viste XML restituiscono query SQL sulle tabelle sottostanti.  
  
## <a name="see-also"></a>Vedere anche  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
