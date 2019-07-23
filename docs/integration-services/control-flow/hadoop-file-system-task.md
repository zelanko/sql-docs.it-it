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
ms.openlocfilehash: 0b75f26a4eae2643ebec512492788bcc60102648
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988167"
---
# <a name="hadoop-file-system-task"></a>Attività File system Hadoop

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
  
