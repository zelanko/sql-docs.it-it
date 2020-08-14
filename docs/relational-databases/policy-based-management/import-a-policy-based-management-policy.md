---
title: Importare i criteri della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54e0ca12595b0ce8bdde128c9261918c910ffdcf
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934348"
---
# <a name="import-a-policy-based-management-policy"></a>Importare i criteri della gestione basata su criteri
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento verrà descritto come importare un'istanza dei criteri della gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Autorizzazioni
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.

  
##  <a name="using-sql-server-management-studio"></a>Utilizzare SQL Server Management Studio  
  
### <a name="to-import-a-policy-instance"></a>Per importare un'istanza dei criteri  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si troverà l'istanza dei criteri appena importata.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Criteri** e selezionare **Importa criteri**.  
  
5.  Nella finestra di dialogo **Importa** digitare il percorso e il nome del file oppure usare il pulsante Sfoglia (**...**) per trovare il file XML che contiene i criteri, quindi selezionare il file. Per ulteriori informazioni sulle opzioni disponibili nella finestra di dialogo **Importa** , vedere [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Al termine, fare clic su **OK**.  


## <a name="example-policies"></a>Criteri di esempio
 I criteri di esempio non sono inclusi nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], ma è possibile accedere ai criteri di esempio precedentemente distribuiti installando [SQL Server Management Studio v17](../../ssms/release-notes-ssms.md#previous-ssms-releases).  Dopo aver installato SQL Server Management Studio v17, è possibile trovare i criteri di esempio in `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies`. Questi criteri possono essere importati e usati come base per criteri di gestione basati su criteri personalizzati.
