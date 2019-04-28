---
title: Seleziona pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 026c588f2fc35a6cb256a63046ad91e5d1b5641a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830248"
---
# <a name="select-a-package"></a>Seleziona pacchetto
  Utilizzare la finestra di dialogo **Seleziona pacchetto** per specificare il pacchetto da cui l'attività Message Queue può ricevere messaggi.  
  
## <a name="static-options"></a>Opzioni statiche  
 **Percorso**  
 Consente di specificare il percorso del pacchetto. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Impostare il percorso su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona questo valore vengono visualizzate le opzioni dinamiche **Server**, **Usa autenticazione di Windows**, **Usa autenticazione di SQL Server**, **Nome utente**e **Password**.|  
|File DTSX|Consente di impostare il percorso su un file DTSX. Se si seleziona questo valore viene visualizzata l'opzione dinamica **Nome file**.|  
  
## <a name="location-dynamic-options"></a>Opzioni dinamiche relative al percorso  
  
### <a name="location--sql-server"></a>Percorso = SQL Server  
 **Nome pacchetto**  
 Consente di selezionare un pacchetto archiviato nel server specificato.  
  
 **Server**  
 Consente di specificare il nome del server o di selezionarlo nell'elenco.  
  
 **Usa autenticazione di Windows**  
 Fare clic su questa opzione per utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione di SQL Server**  
 Fare clic su questa opzione per usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Nome utente**  
 Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare il nome utente da usare per l'accesso al server.  
  
 **Password**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare una password.  
  
### <a name="location--dtsx-file"></a>Percorso = File DTSX  
 **Nome file**  
 Specificare il percorso di un pacchetto oppure fare clic sul pulsante Sfoglia **(...)** per trovare il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Message Queue](message-queue-task.md)  
  
  
