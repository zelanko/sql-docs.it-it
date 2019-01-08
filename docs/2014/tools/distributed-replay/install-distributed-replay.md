---
title: Installare riesecuzione distribuita dal Prompt dei comandi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67d74db6faf9b40ad323ed2948c2c0a596a63016
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816063"
---
# <a name="install-distributed-replay-from-the-command-prompt"></a>Installare Riesecuzione distribuita dal prompt dei comandi
  L'installazione di una nuova istanza di Riesecuzione distribuita dal prompt dei comandi consente di specificare le funzionalità da installare e le relative modalità di configurazione. L'installazione dal prompt dei comandi supporta l'installazione, il ripristino, l'aggiornamento e la disinstallazione dei componenti Riesecuzione distribuita. Quando l'installazione viene eseguita tramite il prompt dei comandi, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata la modalità non interattiva completa tramite il parametro /Q.  
  
> [!NOTE]  
>  Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.  
  
## <a name="installation-parameters"></a>Parametri di installazione  
 L'elenco delle funzionalità di livello principale include [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e Strumenti. La funzionalità Strumenti installa gli strumenti di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e altri componenti condivisi. Per installare i componenti Riesecuzione distribuita, specificare i parametri seguenti:  
  
|Componente|Parametro|  
|---------------|---------------|  
|Controller di Riesecuzione distribuita|**DREPLAY_CTLR**|  
|Client Riesecuzione distribuita|**DREPLAY_CLT**|  
|Strumento di amministrazione|**Strumenti**|  
  
> [!IMPORTANT]  
>  Dopo aver installato i componenti Riesecuzione distribuita, è necessario creare regole del firewall nei computer controller e client e concedere a ogni computer client autorizzazioni nel server di destinazione. Per altre informazioni, vedere [Completare i passaggi successivi all'installazione](complete-the-post-installation-steps.md).  
  
 Utilizzare i parametri elencati nella tabella seguente per sviluppare script della riga di comando per l'installazione.  
  
|Parametro|Descrizione|Valori supportati|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **Facoltativo**|Account del servizio per controller di Riesecuzione distribuita.|Vengono controllati l'account e la password|  
|/CTLRSVCPASSWORD<br /><br /> **Facoltativo**|Password per l'account del servizio controller di Riesecuzione distribuita.|Vengono controllati l'account e la password|  
|/CTLRSTARTUPTYPE<br /><br /> **Facoltativo**|Tipo di avvio per il servizio controller di Riesecuzione distribuita.|Automatico<br /><br /> Disabilitata<br /><br /> Manual|  
|/CTLRUSERS<br /><br /> **Facoltativo**|Specifica gli utenti che dispongono di autorizzazioni per il servizio controller di Riesecuzione distribuita.|Set di stringhe di account utente in cui vengono usati i caratteri " " (spazio) come delimitatore<br /><br /> **Importante**: Quando si configura il servizio Distributed Replay controller, è possibile specificare uno o più account utente che verrà utilizzato per eseguire i servizi client riesecuzione distribuita. Di seguito viene fornito l'elenco degli account supportati:<br /><br /> Account utente di dominio<br /><br /> Account utente locale creato dall'utente<br /><br /> Amministratore<br /><br /> Account virtuale e account del servizio gestito<br /><br /> Servizi di rete, Servizi locali e Sistema<br /><br /> <br /><br /> Gli account di gruppo (locale o dominio) e gli altri account predefiniti (come Everyone) non sono accettati.|  
|/CLTSVCACCOUNT<br /><br /> **Facoltativo**|Account del servizio per client Riesecuzione distribuita.|Vengono controllati l'account e la password|  
|/CLTSVCPASSWORD<br /><br /> **Facoltativo**|Password per l'account del servizio client Riesecuzione distribuita.|Vengono controllati l'account e la password|  
|/CLTSTARTUPTYPE<br /><br /> **Facoltativo**|Tipo di avvio per il servizio client Riesecuzione distribuita.|Automatico<br /><br /> Disabilitata<br /><br /> Manual|  
|/CLTCTLRNAME<br /><br /> **Facoltativo**|Nome del computer con cui il client comunica per il servizio controller di Riesecuzione distribuita.||  
|/CLTWORKINGDIR<br /><br /> **Facoltativo**|Directory di lavoro per il servizio client Riesecuzione distribuita.|Percorso valido|  
|/CLTRESULTDIR<br /><br /> **Facoltativo**|Directory dei risultati per il servizio client Riesecuzione distribuita.|Percorso valido|  
  
### <a name="sample-syntax"></a>Sintassi di esempio:  
 **Per installare il componente Controller di Riesecuzione distribuita**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **Per installare il componente Client Riesecuzione distribuita**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
  
