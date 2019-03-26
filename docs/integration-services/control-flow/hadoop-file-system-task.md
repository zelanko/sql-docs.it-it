---
title: Attività File system Hadoop | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 87dd03cb63da117f3d754cdc9692310e9633e70d
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290737"
---
# <a name="hadoop-file-system-task"></a>Attività File system Hadoop
  L'attività File system Hadoop consente a un pacchetto SSIS di copiare file da, a o all'interno di un cluster Hadoop.  
  
 Per aggiungere un'attività File system Hadoop, trascinarla e rilasciarla nella finestra di progettazione. Fare doppio clic sull'attività o fare clic con il pulsante destro del mouse e scegliere **Modifica**per aprire la finestra di dialogo **Editor attività File system Hadoop** .  
  
 ![Editor attività File system Hadoop](../../integration-services/control-flow/media/hadoop-filesystem-task.png "Editor attività File system Hadoop")  
  
## <a name="options"></a>Opzioni  
 Configurare le opzioni seguenti nella finestra di dialogo **Editor attività File system Hadoop** .  
  
|Campo|Descrizione|  
|-----------|-----------------|  
|**Connessione Hadoop**|Specificare un'istanza esistente di Gestione connessione Hadoop o crearne una nuova. Questa istanza di Gestione connessione indica dove sono ospitati i file di destinazione.|  
|**Percorso del file Hadoop**|Specificare il percorso file o directory in HDFS.|  
|**Tipo di file Hadoop**|Specificare se l'oggetto del File system HDFS è un file o una directory.|  
|**Sovrascrivere la destinazione**|Specificare se sovrascrivere il file di destinazione, se già presente.|  
|**Operazione**|Specificare l'operazione. Le operazioni disponibili sono **CopyToHDFS**, **CopyFromHDFS**e **CopyWithinHDFS**.|  
|**Connessione al file locale**|Specificare un'istanza esistente di Gestione connessione file o crearne una nuova. Questa istanza di Gestione connessione indica dove sono ospitati i file di origine.|  
|**Ricorsivo**|Specificare se copiare in modo ricorsivo tutte le sottocartelle.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione connessione Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
