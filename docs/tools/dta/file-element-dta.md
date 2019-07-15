---
title: Elemento File (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c24484db4d106e236166a2a522a3b038a0b899ec
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727703"
---
# <a name="file-element-dta"></a>Elemento File (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Specifica il file del carico di lavoro. Un carico di lavoro è un set di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sui database che si desidera ottimizzare. I file del carico di lavoro possono essere costituiti da script [!INCLUDE[tsql](../../includes/tsql-md.md)] (sql) o file di traccia (trc). Per altre informazioni, vedere[Avviare e usare Ottimizzazione guidata motore di database](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Usare il tipo di dati **string** per specificare il percorso della directory del file del carico di lavoro. Esempio:<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> Si noti che il limite della lunghezza viene forzato dal server.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Obbligatorio una sola volta se non viene specificato un altro tipo di carico di lavoro. È necessario specificare un elemento figlio **EventString**, **File**o **Database** per l'elemento padre **Workload** , ma è possibile utilizzare un solo tipo. Se ad esempio si specifica un carico di lavoro con l'elemento **File** , non sarà possibile specificare anche un carico di lavoro con l'elemento **Database** nello stesso file di input XML.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Workload &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementi figlio**|Nessuna.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML semplice &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
