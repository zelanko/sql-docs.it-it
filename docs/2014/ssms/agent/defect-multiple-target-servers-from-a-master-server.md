---
title: Escludere più server di destinazione da un server master | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0123027ac9aa87d616b52ac5cc26f36a20f7e1e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62524015"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Escludere più server di destinazione da un server master
  In questo argomento viene illustrata la procedura per l'esclusione di più server di destinazione da una configurazione di amministrazione multiserver in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Eseguire questa procedura dal server master.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>Per escludere più server di destinazione da un server master  
  
1.  In **Esplora oggetti**espandere un server configurato come server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Gestione server di destinazione**.  
  
3.  Fare clic su **Invia istruzioni**e quindi selezionare **Escludi** nell'elenco **Tipo istruzione**.  
  
4.  In **Destinatari**eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Tutti i server di destinazione** per escludere tutti i server di destinazione di questo server master. Questa opzione consente di disinstallare completamente l'attuale configurazione di amministrazione multiserver.  
  
    -   Fare clic su **Solo i server di destinazione seguenti**e quindi sulla casella **Seleziona** corrispondente per escludere solo alcuni server di destinazione di questo server master.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un ambiente multiserver](create-a-multiserver-environment.md)   
 [Amministrazione automatizzata in un'organizzazione](automated-administration-across-an-enterprise.md)   
 [Escludere un server di destinazione da un server master](defect-a-target-server-from-a-master-server.md)  
  
  
