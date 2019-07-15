---
title: Esempio di file di input XML con carico di lavoro inline (DTA) | Microsoft Docs
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
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5cc30a19303aea9db0e989186df820405ddb1384
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731711"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>Esempio di file di input XML con carico di lavoro inline (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Copiare e incollare questo esempio di file di input XML che specifica un carico di lavoro con l'elemento **EventString** nell'editor XML o nell'editor di testo preferito. È possibile utilizzare l'elemento **EventString** per specificare il carico di lavoro di uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] nel file XML invece di utilizzare un file del carico di lavoro separato. Dopo aver copiato questo esempio nello strumento di modifica desiderato, sostituire i valori specificati per gli elementi **Server**, **Database**, **Schema**, **Table**, **Workload**, **EventString**e **TuningOptions** con i valori per la sessione di ottimizzazione specifica. Per altre informazioni su tutti gli attributi e gli elementi figlio che è possibile usare con questi elementi, vedere [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md). Nell'esempio seguente viene utilizzato solo un subset delle opzioni relative agli attributi e agli elementi figlio disponibili.  
  
## <a name="code"></a>codice  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../tools/dta/codesnippet/xml/xml-input-file-sample-wi_1.xml)]  
  
## <a name="comments"></a>Commenti  
 `USE database_name` nel carico di lavoro inline contenuto nell'elemento **EventString** .  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e utilizzo di Ottimizzazione guidata motore di database](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Visualizzare e utilizzare l'output di Ottimizzazione guidata motore di database](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
