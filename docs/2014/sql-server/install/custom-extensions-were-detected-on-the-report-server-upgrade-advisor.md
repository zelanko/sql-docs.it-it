---
title: Sono state rilevate estensioni personalizzate nel server di report (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f985f41104dd194d851760c3d1c3e5479a65b7e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952590"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>Estensioni personalizzate rilevate nel server di report (Upgrade Advisor)
  Nei file di configurazione sono state rilevate impostazioni di estensioni personalizzate, indicanti che l'installazione include una o più estensioni personalizzate per l'elaborazione dati, il recapito, il rendering, la sicurezza o l'autenticazione. In seguito all'aggiornamento le impostazioni di configurazione delle estensioni verranno spostate con il server di report aggiornato. Tuttavia, se le estensioni personalizzate sono installate nella cartella di installazione del server di report esistente, i file di assembly per tali estensioni non verranno spostate nella nuova cartella di installazione durante il processo di aggiornamento. Dopo che l'aggiornamento è stato completato, è necessario spostare i file di assembly nella nuova cartella di installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità SharePoint di.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce un'architettura estensibile che consente agli sviluppatori di creare estensioni personalizzate per l'elaborazione dei dati, il recapito, il rendering, la sicurezza e l'autenticazione.  
  
 Se nell'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono presenti estensioni o assembly personalizzati, è possibile utilizzare il programma di installazione per eseguire un aggiornamento, ma potrebbe essere necessario spostare le estensioni nel nuovo percorso di installazione dopo il completamento dell'aggiornamento oppure eseguire altri passaggi prima dell'aggiornamento.  
  
> [!NOTE]  
>  Preparazione aggiornamento non è in grado di rilevare se assembly di codice personalizzati sono configurati per essere utilizzati in report per il calcolo di valori, stili e formattazione degli elementi. Per ulteriori informazioni, vedere [altri Reporting Services problemi di aggiornamento](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md).  
  
 Se sono state acquistate estensioni personalizzate, contattare il fornitore del software per verificare se sono disponibili ulteriori informazioni sull'aggiornamento della funzionalità personalizzata.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Utilizzare le sezioni seguenti per determinare i passaggi da eseguire in aggiunta o prima dell'esecuzione di un aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 [Estensioni per l'elaborazione dati o per il recapito personalizzate](#dataprocdeliver)  
  
 [Estensioni per il rendering personalizzate](#render)  
  
 [Estensioni di sicurezza o di autenticazione personalizzate in un server di report SQL Server 2000](#secauth2000)  
  
 [Estensioni di sicurezza o di autenticazione personalizzate in un server di report di SQL Server 2005](#secauth2005)  
  
 Dopo che l'aggiornamento è stato completato, spostare gli assembly delle estensioni nella nuova cartella di installazione, quindi verificare che le estensioni personalizzate funzionino nel modo previsto. Se l'estensione non funziona, può essere necessario ricompilarla.  
  
#### <a name="to-recompile-an-extension"></a>Per ricompilare un'estensione  
  
1.  Copiare il file Microsoft.ReportingServices.Interfaces.dll nella cartella che contiene il codice sorgente.  
  
2.  Aprire il progetto che contiene i file di origine e aggiunge un riferimento al file Microsoft.ReportingServices.Interfaces.dll.  
  
3.  Ricompilare la soluzione per associare l'estensione.  
  
 Se non si intende continuare l'aggiornamento, è possibile decidere di eseguire la migrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per i passaggi relativi alla migrazione di estensioni personalizzate, vedere [migrazione di estensioni personalizzate](#migrcustext) in questo argomento.  
  
###  <a name="dataprocdeliver"></a>Estensioni per il recapito o l'elaborazione dati personalizzate  
 Se Preparazione aggiornamento rileva estensioni per l'elaborazione dati o per il recapito personalizzate, il processo di aggiornamento non viene bloccato. Una volta completato l'aggiornamento, potrebbe tuttavia essere necessario eseguire passaggi aggiuntivi prima di poter utilizzare la funzionalità personalizzata fornita da tali estensioni. È necessario ad esempio eseguire passaggi aggiuntivi quando i file dell'estensione personalizzata vengono installati nella cartella di installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>Passaggi successivi all'aggiornamento per le estensioni per l'elaborazione dati o per il recapito personalizzate  
  
1.  Spostare il file o i file di estensione nella nuova cartella di programma per il server di report. Per impostazione predefinita, la cartella del programma del server di report è \Programmi\microsoft SQL Server \ MSRS10_50. \< *instance_name*> server \Report.  
  
 Per ulteriori informazioni, vedere le sezioni relative alla distribuzione di estensioni per l'elaborazione dati e il recapito nella documentazione online di SQL Server.  
  
###  <a name="render"></a>Estensioni per il rendering personalizzate  
 Se Preparazione aggiornamento rileva estensioni per il rendering personalizzate, il processo di aggiornamento viene bloccato. È possibile continuare il processo di aggiornamento rimuovendo le voci di configurazione dell'estensione personalizzata dal file di configurazione. In questo caso tuttavia le estensioni personalizzate non saranno disponibili per gli utenti dopo che l'aggiornamento è stato completato. Se dopo l'aggiornamento sono necessarie estensioni per il rendering personalizzate, è necessario compilare estensioni per il rendering aggiornate oppure ottenerle da un fornitore.  
  
 È necessario eseguire alcuni passaggi per abilitare un aggiornamento oppure è possibile eseguire la migrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Non eseguire l'aggiornamento né la migrazione del server di report fino a quando non è stato testato e verificato che il funzionamento dell'estensione per il rendering aggiornata è quello previsto.  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>Per aggiornare estensioni per il rendering personalizzate  
  
1.  Ottenere estensioni per il rendering con le interfacce più recenti.  
  
2.  Rimuovere la voce o le voci dell'estensione per il rendering personalizzata obsoleta dal file RSReportServer.config.  
  
3.  Aggiornare il server di report.  
  
4.  Dopo che l'aggiornamento è stato completato, installare le estensioni aggiornate nel server di report.  
  
 Per ulteriori informazioni, vedere la sezione relativa all'implementazione di un'estensione per il rendering nella documentazione online di SQL Server.  
  
###  <a name="secauth2000"></a>Estensioni di sicurezza o di autenticazione personalizzate in un server di report SQL Server 2000  
 Se Preparazione aggiornamento rileva estensioni di sicurezza o di autenticazione personalizzate in un server di report di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], il processo di aggiornamento viene bloccato. È necessario eseguire alcuni passaggi per abilitare un aggiornamento oppure è possibile eseguire la migrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. In entrambi i casi è necessario aggiornare e ricompilare le estensioni con le interfacce più recenti in Microsoft.ReportingServices.Interfaces.dll, poiché le interfacce sono state modificate in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] rispetto a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
> [!IMPORTANT]  
>  Non eseguire l'aggiornamento né la migrazione del server di report fino a quando non è stato testato e verificato che il funzionamento dell'estensione di sicurezza o di autenticazione aggiornata è quello previsto.  
  
 se si utilizza un'estensione di autenticazione personalizzata creata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario modificare il codice sorgente per supportare le nuove classi e i nuovi membri introdotti per i report basati su modello.  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>Per aggiornare le estensioni di sicurezza o di autenticazione personalizzate da un server di report SQL Server 2000  
  
1.  Aggiornare e ricompilare qualsiasi estensione di sicurezza o di autenticazione con le interfacce più recenti.  
  
2.  Rimuovere la voce o le voci dell'estensione di sicurezza o di autenticazione personalizzata dal file RSReportServer.config.  
  
3.  Aggiornare il server di report.  
  
4.  Dopo che l'aggiornamento è stato completato, installare le estensioni aggiornate nel server di report.  
  
 Per ulteriori informazioni, vedere la sezione relativa all'implementazione di un'estensione di sicurezza nella documentazione online di SQL Server.  
  
###  <a name="secauth2005"></a>Estensioni di sicurezza o di autenticazione personalizzate in un server di report SQL Server 2005  
 Se Preparazione aggiornamento rileva estensioni di sicurezza o di autenticazione personalizzate in un server di report di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], il processo di aggiornamento viene bloccato. È necessario eseguire alcuni passaggi per abilitare un aggiornamento oppure è possibile eseguire la migrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>Per aggiornare estensioni di sicurezza o di autenticazione personalizzate da un server di report di SQL Server 2005  
  
1.  Rimuovere la voce o le voci di configurazione dell'estensione di sicurezza o di autenticazione personalizzata dal file RSReportServer.config.  
  
2.  Aggiornare il server di report.  
  
3.  Dopo che l'aggiornamento è stato completato, aggiungere nuovamente le voci di configurazione nel file RSReportServer.config.  
  
4.  Se gli assembly dell'estensione sono installati nella cartella di installazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] obsoleta, spostarsi nella nuova cartella di installazione.  
  
 Per ulteriori informazioni, vedere la sezione relativa all'implementazione di un'estensione di sicurezza nella documentazione online di SQL Server.  
  
###  <a name="migrcustext"></a>Migrazione di estensioni personalizzate  
 Se si decide di eseguire la migrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anziché un aggiornamento, utilizzare i passaggi per eseguire la migrazione delle estensioni personalizzate alla nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>Per eseguire la migrazione delle estensioni personalizzate a una nuova istanza di Reporting Services  
  
1.  Compilare oppure ottenere estensioni aggiornate con le interfacce di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] più recenti.  
  
2.  Eseguire la migrazione del server di report a una nuova istanza.  
  
3.  Configurare le estensioni nella nuova istanza.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
