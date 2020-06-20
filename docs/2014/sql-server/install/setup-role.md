---
title: Impostazione del ruolo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
ms.openlocfilehash: 555c6946a9732d478d9e7dca76b84ce17d0e90e2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036274"
---
# <a name="setup-role"></a>Impostazione ruolo
  Utilizzare questa pagina per specificare se utilizzare la pagina Selezione funzionalità per selezionare le funzionalità singole oppure eseguire l'installazione tramite un ruolo di installazione.  
  
 Il `setup role` è una selezione predefinita di tutte le funzionalità e di tutti i componenti condivisi necessari per implementare una configurazione predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Installazione funzionalità**  
 Scegliere questa opzione per selezionare le funzionalità singole e i componenti condivisi. Le funzionalità dell'istanza includono Servizi Motore di database, Analysis Services (modalità nativa) e Reporting Services.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerPivot per SharePoint**  
 Scegliere questa opzione per installare i componenti del server Analysis Services in una farm SharePoint 2010. Questa opzione consente di distribuire il servizio di sistema PowerPivot e il server Analysis Services in una farm, abilitando l'elaborazione di dati e query per cartelle di lavoro di Excel pubblicate che contengono dati di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incorporati.  
  
 Se necessario, è possibile aggiungere un'istanza del motore di database relazionale all'installazione per ospitare i database in una farm di SharePoint. Se la farm è già configurata, è possibile ignorare questa opzione.  
  
 Al termine dell'installazione, è necessario configurare il software utilizzando uno degli approcci seguenti: strumento di configurazione PowerPivot, cmdlet di PowerShell o Amministrazione centrale SharePoint 2010. A differenza delle versioni precedenti, durante l'installazione non viene più eseguita alcuna attività di configurazione per un'installazione di PowerPivot.  
  
 In un'installazione basata su ruoli non è incluso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot per l'applicazione client di Excel. L'applicazione client viene installata separatamente.  
  
 **Tutte le funzionalità con valori predefiniti**  
 Scegliere questo ruolo per installare tutte le funzionalità disponibili per questa versione. Si noti che PowerPivot per SharePoint è escluso da questo ruolo. È necessario utilizzare il ruolo di installazione PowerPivot per SharePoint per installare tale funzionalità.  
  
 Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è configurato per l'avvio tramite l'account **NT AUTHORITY\NETWORK SERVICE** . Per l'utente corrente viene eseguito il provisioning come membro del ruolo **sysadmin** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile eseguire l'override dei valori impostati con questa opzione specificando i parametri della riga di comando aggiuntivi.  
  
 Quando il sistema operativo non è un controller di dominio, per impostazione predefinita nel motore di database e in Reporting Services verrà utilizzato l'account NTAUTHORITY\NETWORK SERVICE, in Integration Services l'account NTAUTHORITY\NETWORK SERVICE e nell'Utilità di avvio del daemon filtri full-text di SQL l'account NTAUTHORITY\LOCAL SERVICE.  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di PowerPivot per SharePoint](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [Requisiti hardware e software (PowerPivot per SharePoint](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [Selezione delle funzioni](../../../2014/sql-server/install/feature-selection.md)  
  
  
