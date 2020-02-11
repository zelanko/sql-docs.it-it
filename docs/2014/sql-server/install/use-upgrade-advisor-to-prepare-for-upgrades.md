---
title: Utilizzare Preparazione aggiornamento per preparare gli aggiornamenti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab9c51ba125a7489d693a1af6b16e432e8fb7099
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632730"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>Utilizzare Preparazione aggiornamento per preparare gli aggiornamenti
  Preparazione aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] semplifica le attività di preparazione per l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Preparazione aggiornamento consente di analizzare i componenti installati dalle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di generare un report contenente i problemi da correggere prima o dopo l'aggiornamento.  
  
## <a name="how-upgrade-advisor-works"></a>Funzionamento di Preparazione aggiornamento  
 Quando si esegue Preparazione aggiornamento, ne viene visualizzata l'home page, da cui è possibile eseguire gli strumenti seguenti:  
  
-   Analisi guidata di Preparazione aggiornamento  
  
-   Visualizzatore report di Preparazione aggiornamento  
  
-   Guida di Preparazione aggiornamento  
  
 La prima volta che si utilizza Preparazione aggiornamento, eseguire l'Analisi guidata di Preparazione aggiornamento per analizzare i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al termine dell'analisi, visualizzare i report risultanti nel Visualizzatore report di Preparazione aggiornamento. In ogni report sono inclusi collegamenti a informazioni della Guida di Preparazione aggiornamento che consentono di correggere o ridurre gli effetti dei problemi noti.  
  
## <a name="upgrade-advisor-analysis"></a>Analisi di Preparazione aggiornamento  
 Preparazione aggiornamento analizza i seguenti componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 Nell'analisi vengono esaminati gli oggetti a cui è possibile accedere, quali script, stored procedure, trigger e file di traccia. Preparazione aggiornamento non è in grado di analizzare applicazioni desktop o stored procedure crittografate.  
  
 L'output è nel formato di un report XML. Per visualizzare il report XML, utilizzare il Visualizzatore report di Preparazione aggiornamento.  
  
> [!NOTE]  
>  I report potrebbero contenere l'indicazione di altri problemi di aggiornamento non rilevati da Preparazione aggiornamento ma che potrebbero esistere sul server o nelle applicazioni. Esaminare l'elenco dei problemi non rilevabili e determinare se sia necessario apportare modifiche al server o alle applicazioni a causa di tali problemi.  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>Come installare e aggiornare Preparazione aggiornamento  
 Il percorso di installazione di Preparazione aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende dagli elementi analizzati. Preparazione aggiornamento supporta l'analisi remota di tutti i componenti supportati, ad eccezione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se non si esegue l'analisi di istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile installare Preparazione aggiornamento in qualsiasi computer in grado di connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e che soddisfa i prerequisiti di Preparazione aggiornamento. Per ulteriori informazioni, vedere [aggiornamenti di versione ed edizione supportati](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Se si prevede di analizzare le istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario installare Preparazione aggiornamento nel server di report.  
  
 Preparazione aggiornamento è disponibile in un feature pack.  
  
 Di seguito vengono indicati i prerequisiti per l'installazione e l'esecuzione di Preparazione aggiornamento:  
  
-   
  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, Windows 7 SP1 e [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1.  
  
-   Windows Installer a partire dalla versione 4.5. È possibile installare Windows Installer dal [sito Web di Windows Installer](https://www.microsoft.com/download/details.aspx?id=8483).  
  
-   Microsoft .NET Framework 4. .NET Framework 4 è disponibile sul supporto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del prodotto e dalla pagina di [download di .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=209895).  
  
    -   Per eseguire l'installazione di .NET Framework 4 dai supporti di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], individuare la radice dell'unità disco. Fare quindi doppio clic sulla cartella \redist, sulla cartella DotNetFrameworks ed eseguire dotNetFx40_Full_x86_x64.exe (sia per i sistemi operativi a 32 bit che per quelli a 64 bit).  
  
 Per installare Preparazione aggiornamento dal Web, fare clic sul pulsante di download presente nella pagina di download. È quindi possibile eseguire l'installazione immediatamente oppure salvare il file SQLUA.msi per eseguirlo successivamente. Se l'installazione viene eseguita dal disco del prodotto, eseguire SQLUA.msi direttamente da tale disco.  
  
 Dopo aver installato Preparazione aggiornamento, è possibile aprirlo dal menu **Start** :  
  
-   Fare clic sul pulsante **Start**, scegliere **tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], quindi fare clic su ** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] preparazione aggiornamento**.  
  
 Per ulteriori informazioni, vedere la documentazione inclusa nel download di Preparazione aggiornamento e le note sulla versione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Usare più versioni e istanze di SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Aggiornamenti di versione ed edizione supportati](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilità con le versioni precedenti](../../../2014/getting-started/backward-compatibility.md)  
  
  
