---
title: Schema di memorizzazione nella cache (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ca536125be481766e41c3665dd313d483160ae0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013283"
---
# <a name="schema-caching-sqlxml-40"></a>Memorizzazione nella cache degli schemi (SQLXML 4.0)
  Con un'installazione side-by-side di XML per Microsoft SQL Server 2000 Web Release 1, Microsoft SQLXML 2.0 e SQLXML 3.0, è possibile controllare in modo esplicito lo schema di memorizzazione nella cache in tutte le versioni utilizzando le seguenti chiavi del Registro di sistema:  
  
 Web Release 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Per ulteriori informazioni sull'installazione side-by-side, vedere [novità di SQLXML 4.0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 La memorizzazione nella cache degli schemi migliora notevolmente le prestazioni di una query XPath. Quando una query XPath viene eseguita su uno schema di mapping, lo schema viene archiviato in memoria e le strutture dei dati necessarie vengono incluse in memoria. Se la memorizzazione nella cache degli schemi è impostata, lo schema resta in memoria e comporta un miglioramento delle prestazioni per le query XPath successive.  
  
 È possibile impostare le dimensioni della cache degli schemi aggiungendo nel Registro di sistema la chiave sopra riportata.  
  
 Le dimensioni dello schema vengono impostate in base sulla memoria disponibile e al numero di schemi utilizzati. Il valore predefinito **SchemaCacheSize** dimensioni sono 31. Se si imposta **SchemaCacheSize** superiore, viene utilizzata più memoria. Pertanto, è possibile aumentare le dimensioni della cache se l'accesso allo schema sembra lento o ridurle se la memoria è insufficiente.  
  
 Per motivi di prestazioni, è consigliabile impostare **SchemaCacheSize** maggiore del numero di schemi di mapping utilizzati normalmente. Come aumenta il numero di schemi, se **SchemaCacheSize** è minore rispetto al numero di schemi è, le prestazioni peggiorano.  
  
> [!NOTE]  
>  Durante lo sviluppo, è consigliabile non memorizzare nella cache gli schemi, in quanto le modifiche apportate agli schemi non vengono riflesse nella cache per circa due minuti.  
  
## <a name="see-also"></a>Vedere anche  
 [La cache dei modelli &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [La memorizzazione nella cache di XSL &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
