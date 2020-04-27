---
title: Avvia Generatore report (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fc123be862320cd35ccf4aec76d8bc9cf7877af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107595"
---
# <a name="start-report-builder-report-builder"></a>Avviare Generatore report (Generatore report).
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]include le versioni autonome [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] e di Generatore report. È possibile utilizzare la versione [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato in modalità nativa o in modalità integrata SharePoint.  
  
> [!NOTE]  
>  Generatore report non può essere installato in computer basati sul processore Itanium 64. Questa regola si applica sia alla versione [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] sia a quella autonoma di Generatore report.  
  
 Se la versione [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] di Generatore report avviata è una versione precedente, contattare l'amministratore, che potrà aggiornare Gestione report e il sito di SharePoint per consentire l'utilizzo della versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di Generatore report.  
  
 È possibile utilizzare anche la versione [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] di Generatore report per creare report nella cartella di lavoro [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] pubblicata su SharePoint. Per ulteriori informazioni sull'utilizzo di Generatore report [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]con, vedere la pagina relativa alla [creazione di un report Reporting Services con dati PowerPivot](https://go.microsoft.com/fwlink/?LinkId=185238) in TechNet.Microsoft.com.  
  
 Per avviare Generatore report autonomo dal menu **Start** nel computer locale, l'utente o un amministratore deve installare Generatore report direttamente nel computer prima che lo strumento sia disponibile per l'utilizzo. La versione autonoma non viene installata quando si installa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ma è necessario scaricarla e installarla separatamente. Per scaricare Generatore report, vedere [Microsoft® SQL Server® 2012 Generatore report](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>Per avviare Generatore report ClickOnce da Gestione report  
  
1.  Digitare l'URL per il server di report nella barra degli indirizzi del browser. Per impostazione predefinita, l'URL è\<http://*nomeserver*>/Reports. Verrà aperto Gestione report.  
  
2.  Fare clic su **Generatore report**.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>Per avviare Generatore report ClickOnce tramite un URL  
  
1.  Nella barra degli indirizzi del browser digitare l'URL seguente:  
  
     http://\<nomeserver>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application  
  
2.  Premere INVIO.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>Per avviare Generatore report ClickOnce in modalità integrata SharePoint  
  
1.  Accedere al sito di SharePoint che contiene la raccolta desiderata.  
  
2.  Aprire la raccolta.  
  
3.  Fare clic su **Documenti**.  
  
4.  Scegliere **Report di Generatore report** dal menu **Nuovo documento**.  
  
     Verrà avviato Generatore report e sarà possibile creare un report o aprire un report nel server di report.  
  
     **Nota** Se nel menu **nuovo documento** non sono elencate le opzioni **report Generatore report**, **modello Generatore report**e **origine dati report** , i relativi tipi di contenuto devono essere aggiunti alla raccolta di SharePoint. Per ulteriori informazioni, vedere [aggiungere tipi di contenuto del server di report a una raccolta &#40;Reporting Services in modalità integrata SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md) nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [documentazione online](https://go.microsoft.com/fwlink/?LinkId=154888) di MSDN.Microsoft.com.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>Per avviare la versione autonoma di Generatore report dal menu Start  
  
1.  Dal menu Start fare clic su **tutti i programmi**, quindi fare [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] clic su **Generatore report**.  
  
2.  Fare clic su **Generatore report** .  
  
     Verrà visualizzato Generatore report e sarà possibile creare o aprire un report.  
  
3.  Per creare un nuovo report, fare clic sull'icona di SQL Server nell'angolo superiore sinistro di Generatore report, quindi fare clic su Nuovo.  
  
4.  Per aprire un report esistente archiviato nel computer locale o in un server di report, fare clic sull'icona di SQL Server nell'angolo superiore sinistro di Generatore report, quindi fare clic su Apri.  
  
     Se il server di report non è visibile nell'elenco di server esistenti, chiudere la finestra di dialogo **Apri report** , quindi fare clic su **Connetti** nella parte inferiore di Generatore report per connettersi al server.  
  
## <a name="see-also"></a>Vedi anche  
 [Generatore report in SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
