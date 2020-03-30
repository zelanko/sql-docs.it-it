---
title: Seleziona dispositivo di backup | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c4eb20f4492e3550ffdbfca5a649684e28685c1f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68216179"
---
# <a name="select-backup-device"></a>Seleziona dispositivo di backup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare la finestra di dialogo **Seleziona dispositivo di backup** per selezionare un dispositivo di backup logico per l'operazione di ripristino.  
  
 Un dispositivo di backup logico è un dispositivo logico definito dall'utente che corrisponde a un dispositivo fisico, un'unità nastro o un'unità disco, disponibile tramite il sistema operativo.  
  
> [!NOTE]  
>  Se un backup utilizza più dispositivi di backup, è necessario che tutti corrispondano a un unico tipo di dispositivo.  
  
 **Per utilizzare SQL Server Management Studio per visualizzare il contenuto di un dispositivo di backup**  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 **Dispositivo di backup**  
 Nella casella di riepilogo selezionare il nome di un dispositivo di backup logico dal quale si desidera eseguire il ripristino.  
  
 Per informazioni su come visualizzare il contenuto di un dispositivo di backup, vedere [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## <a name="remarks"></a>Osservazioni  
 Se nell'elenco non è visualizzato un dispositivo di backup logico contenente il backup di interesse, è possibile che il backup sia stato scritto direttamente su uno o più file o unità nastro. In questo caso, chiudere la finestra di dialogo **Seleziona dispositivo di backup** e selezionare **File** o **Nastro** nella casella di riepilogo **Supporti di backup** della finestra di dialogo **Seleziona backup** .  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
