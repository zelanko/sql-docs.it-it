---
title: Impostare le dimensioni massime di un file di traccia (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- size [SQL Server], trace files
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 063cdb883de4abd7b32819449251e6f3dec9f592
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62440278"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>Impostare le dimensioni massime di un file di traccia (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Per impostare le dimensioni massime di un file di traccia, utilizzare la procedura seguente.  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>Per impostare le dimensioni massime di un file di traccia  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia**.  
  
    > [!NOTE]  
    >  Se l'opzione **Avvia traccia non appena viene stabilita una connessione**è selezionata, la finestra di dialogo **Proprietà traccia**non viene visualizzata e viene invece avviata la traccia. Per disabilitare questa impostazione, scegliere **Opzioni**dal menu **Strumenti**e deselezionare la casella di controllo **Avvia traccia non appena viene stabilita una connessione** .  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Nell'elenco **Nome del modello**selezionare un modello di traccia.  
  
4.  Selezionare **Salva nel file**e quindi specificare un file per archiviare le informazioni di traccia.  
  
5.  Nella casella di controllo **Dimensioni massime del file** specificare le dimensioni massime del file di traccia. Quando il file raggiungerà le dimensioni massime specificate, gli eventi di traccia non verranno più registrati in tale file. Se si seleziona la casella di controllo **Consenti rollover dei file** , che è selezionata per impostazione predefinita, si verifica quanto segue:  
  
     Quando il file corrente raggiunge le dimensioni massime, l'opzione di rollover determina la chiusura di tale file in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la creazione di un nuovo file. Le dimensioni del nuovo file corrispondono a quelle del file precedente ma viene aggiunto un numero intero al nome per indicare la relativa sequenza. Se ad esempio il file di traccia originale è denominato filename_1.trc, il nome del file di traccia successivo sarà filename_2.trc, e così via. Se il nome assegnato a un nuovo file di rollover è già utilizzato da un file esistente, quest'ultimo verrà sovrascritto a meno che sia di sola lettura. L'opzione di rollover dei file viene abilitata per impostazione predefinita quando si salvano i dati di traccia in un file.  
  
     Con l'opzione di rollover dei file attivata, la traccia continua fino a quando non viene arrestata in qualche altro modo. Per arrestare la traccia dopo che è stato raggiunto il limite delle dimensioni del file, disabilitare l'opzione di rollover.  
  
    > [!NOTE]  
    >  Nel file system FAT32, il limite per le dimensioni dei file è leggermente inferiore a 4 gigabyte (GB). Quando il file di traccia raggiunge tali dimensioni, viene visualizzato il messaggio di errore "Spazio su disco insufficiente". Per creare file di maggiori dimensioni, utilizzare il file system NTFS.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
