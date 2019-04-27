---
title: Installazione degli aggiornamenti dal prompt dei comandi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51ad82519e8afd5e4a871046465e0cafec2f783e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774982"
---
# <a name="installing-updates-from-the-command-prompt"></a>Installazione degli aggiornamenti dal prompt dei comandi
  Provare gli script di installazione e adattarli alle esigenze della propria azienda.  
  
## <a name="sample-syntax-for-installation"></a>Sintassi di esempio per l'installazione  
 Il nome del pacchetto di aggiornamento può variare e includere una lingua, un'edizione e un componente processore. Applicare un aggiornamento dal prompt dei comandi sostituendo <package_name> con il nome del pacchetto di aggiornamento.  
  
-   Aggiornare una singola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tutti i componenti condivisi, quali [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e strumenti di gestione: L'istanza può essere specificata utilizzando il parametro InstanceName o InstanceID. Per aggiornare un'istanza predisposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario specificare il parametro InstanceID<nome_pacchetto>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance o <nome_pacchetto>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<ID istanza>.  
  
-   La configurazione consente di integrare gli aggiornamenti più recenti del pacchetto con l'installazione del prodotto principale, in modo che il prodotto principale e i relativi aggiornamenti applicabili vengano installati contemporaneamente. È possibile preparare un'installazione dell'istanza del motore di database affinché includa l'aggiornamento del prodotto: setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateEnabled=True /UpdateSource=\<percorso in cui viene scaricato l'aggiornamento> /INSTANCEID=\<ID istanza> /FEATURES=SQLEngine.  
  
-   Aggiornare solo i componenti condivisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quali [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti di gestione: <nome_pacchetto>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
  
-   Aggiornare tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel computer e tutti i componenti condivisi, quali [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti di gestione: <nome_pacchetto>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.  
  
 Rimuovere un aggiornamento dal prompt dei comandi sostituendo <nome_pacchetto> con il nome del pacchetto di aggiornamento.  
  
-   Rimuovere un aggiornamento da una singola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e da tutti i componenti condivisi, quali [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti di gestione: <nome_pacchetto>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.  
  
-   Rimuovere un aggiornamento solo dai componenti condivisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quali [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e gli strumenti di gestione: <nome_pacchetto>.exe /qs /Action=RemovePatch  
  
    > [!NOTE]  
    >  Il programma di installazione dell'aggiornamento verifica che la versione dei componenti condivisi sia sempre corrispondente o superiore alla versione dell'istanza di livello più alto.  
  
## <a name="supported-command-prompt-parameters"></a>Parametri del prompt dei comandi supportati  
  
> [!IMPORTANT]  
>  Se possibile, specificare le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file di script, proteggere tale file per impedire l'accesso non autorizzato.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**/?**|Visualizza la Guida del prompt dei comandi per l'installazione automatica|  
|**/action=Patch or /action=RemovePatch**|Specifica l'azione di installazione: Patch o RemovePatch.|  
|**/allinstances**|Applica l'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a tutti i componenti condivisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supportano le istanze.|  
|**/InstanceName = NomeIstanza** <sup>1</sup>|Applica l'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominata InstanceName e a tutti i componenti condivisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supportano le istanze.|  
|**/InstanceID=Inst1**|Applica l'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] all'istanza Inst1 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a tutti i componenti condivisi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supportano le istanze.|  
|**/quiet**|Esegue l'installazione dell'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità automatica.|  
|**/qs**|Visualizza solo la finestra di dialogo dell'interfaccia utente relativa allo stato.|  
|**/UpdateEnabled**|Specifica se durante la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debbano essere individuati e inclusi aggiornamenti del prodotto. I valori validi sono True e False oppure 1 e 0. Per impostazione predefinita, gli aggiornamenti individuati verranno inclusi nel programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**/IAcceptSQLServerLicenseTerms**|Obbligatorio solo quando il parametro /Q o /QS è specificato per le installazioni automatiche.|  
  
 <sup>1</sup> non è possibile specificare questo parametro per applicare un aggiornamento a un'istanza predisposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Specificare il parametro /instanceID.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica sull'installazione dei servizi SQL Server](../../sql-server/install/overview-of-sql-server-servicing-installation.md)  
  
  
