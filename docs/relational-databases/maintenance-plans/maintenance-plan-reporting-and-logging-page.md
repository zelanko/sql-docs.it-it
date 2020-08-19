---
description: Piano di manutenzione (pagina Report e registrazione)
title: Piano di manutenzione (pagina Report e registrazione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05db1c0f8c2eacd2a30e1e1e50b08e090ca6e9c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420865"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>Piano di manutenzione (pagina Report e registrazione)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare la finestra di dialogo **Report e registrazione** per configurare i report e i log generati durante l'esecuzione dei piani di manutenzione.  
  
## <a name="options"></a>Opzioni  
 **Genera report in un file di testo**  
 Consente di specificare se si vuole che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crei un report in un file di testo.  
  
 **Creare un nuovo file**  
 Consente di creare un nuovo file di report per ogni esecuzione del piano di manutenzione. Per impostazione predefinita, i file di report vengono creati nel computer sul quale viene eseguita l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente il piano di manutenzione corrente, nella cartella specificata come cartella dei log predefinita durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per specificare una cartella diversa, immettere il percorso completo nella casella di testo **Cartella** oppure fare clic sul pulsante "**...**" e selezionare la cartella desiderata.  
  
 **Accoda a file**  
 Consente di accodare il report generato da ogni esecuzione del piano al file specificato nella casella di testo **Nome file** . È inoltre possibile specificare un file facendo clic sul pulsante Sfoglia (...) e selezionando un file nella finestra di dialogo visualizzata.  
  
 **Invia report a destinatario di posta elettronica**  
 Consente di trasmettere tramite posta elettronica il risultato dell'esecuzione di un piano di manutenzione. Questa opzione è disponibile solo se l'opzione Posta elettronica database è abilitata e configurata correttamente.  
  
 **Operatore agente**  
 Consente di selezionare un operatore agente nell'elenco come destinatario del messaggio di posta elettronica. Questa opzione è disponibile solo se la posta elettronica è abilitata e configurata correttamente.  
  
 **Registra informazioni estese**  
 Consente di includere maggiori informazioni nel log. Se questa opzione viene selezionata, le dimensioni della cronologia del piano di manutenzione archiviato risulteranno maggiori.  
  
 **Accedi a server remoto**  
 Consente di registrare la cronologia del piano di manutenzione in un server remoto.  
  
 **Connection**  
 Consente di specificare le informazioni di connessione da utilizzare per la registrazione in un server remoto.  
  
 **Nuovo**  
 Consente di visualizzare la finestra di dialogo **Proprietà connessione** . utilizzata per configurare le informazioni per una nuova connessione per la registrazione in un server remoto.  
  
## <a name="see-also"></a>Vedere anche  
 [Piani di manutenzione](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
  
