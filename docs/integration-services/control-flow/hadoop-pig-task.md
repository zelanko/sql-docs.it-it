---
title: Attività Pig Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadooppigtask.f1
ms.assetid: 90646316-9822-48aa-9900-295a33750780
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a624228a0df45ee0ba2954d27e38be511db629fe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294090"
---
# <a name="hadoop-pig-task"></a>Attività Pig Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare l'attività Pig Hadoop per eseguire script Pig in un cluster Hadoop.  
  
 Per aggiungere un'attività Pig Hadoop, trascinarla e rilasciarla nella finestra di progettazione. Fare doppio clic sull'attività o fare clic con il pulsante destro del mouse e scegliere **Modifica**per visualizzare la finestra di dialogo **Editor attività Pig Hadoop** .  
  
 ![Editor attività Pig Hadoop](../../integration-services/control-flow/media/hadoop-pig-task.png "Editor attività Pig Hadoop")  
  
## <a name="options"></a>Opzioni  
 Configurare le opzioni seguenti nella finestra di dialogo **Editor attività Pig Hadoop** .  
  
|Campo|Descrizione|  
|-----------|-----------------|  
|**Connessione Hadoop**|Specificare un'istanza esistente di Gestione connessione Hadoop o crearne una nuova. Questa istanza di Gestione connessione indica dove è ospitato il servizio WebHCat.|  
|**SourceType**|Specificare il tipo di origine della query. I valori disponibili sono **ScriptFile** e **DirectInput**.|  
|**InlineScript**|Quando il valore di **SourceType** è **DirectInput**, specificare lo script Pig.|  
|**HadoopScriptFilePath**|Quando il valore di **SourceType** è **ScriptFile**, specificare il percorso del file di script in Hadoop.|  
|**TimeoutInMinutes**|Specificare un valore di timeout in minuti. Il processo Hadoop viene interrotto se non è stato completato prima del timeout. Specificare 0 per pianificare il processo Hadoop in modo che sia eseguito in modo asincrono.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione connessione Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
