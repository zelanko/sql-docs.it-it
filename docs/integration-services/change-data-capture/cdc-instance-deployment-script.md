---
title: CDC Instance Deployment Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 595af36a5eb19ff6fd019df8a2b9203537350c5a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298902"
---
# <a name="cdc-instance-deployment-script"></a>CDC Instance Deployment Script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Nella finestra di dialogo CDC Instance Deployment Script viene visualizzato lo script di distribuzione dell'istanza di CDC. Questo script può essere usato per ricreare il database CDC con tutti i relativi elementi in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa.  
  
 Al completamento dello script di distribuzione, è necessario accertare le condizioni seguenti:  
  
-   Lo script di distribuzione presuppone che l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione sia stata preparata per Oracle CDC, tramite Oracle CDC Service Configuration Console o lo **script di preparazione** creato dal programma.  
  
-   La parte dello script utilizzata per abilitare il database per CDC deve essere eseguita con il ruolo `sysadmin`.  
  
-   Nello script non viene memorizzata la password di log mining di Oracle. Questa operazione deve essere eseguita manualmente dopo l'esecuzione dello script e l'avvio del servizio CDC.  
  
 Selezionare le opzioni seguenti nella finestra di dialogo **CDC Instance Deployment Script** .  
  
 **Save As**  
 Tramite questa opzione è possibile salvare lo script in un file di testo nel percorso desiderato. È possibile copiare il file con lo script in qualsiasi altro server si desideri eseguirlo.  
  
 **Copia**  
 Tramite questa opzione è possibile copiare lo script negli Appunti. Sarà quindi possibile incollare lo script in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o in qualsiasi editor di testo per eseguirlo in un momento successivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Preparare SQL Server per CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
