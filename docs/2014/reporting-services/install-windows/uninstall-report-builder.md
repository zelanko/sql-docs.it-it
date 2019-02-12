---
title: Disinstallare la versione autonoma di Generatore Report (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 10d6d79587051b78f212c5fbe4a9d866ee0c75e0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014624"
---
# <a name="uninstall-the-stand-alone-version-of-report-builder-report-builder"></a>Disinstallare la versione autonoma di Generatore report (Generatore report)
  È possibile disinstallare la versione autonoma di Generatore report dal Pannello di controllo o dalla riga di comando. Non è possibile disinstallare la versione [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] di Generatore report senza disinstallare [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].  
  
 La sintassi per la disinstallazione di Generatore report dalla riga di comando è identica a quella che si utilizza per l'installazione di Generatore report, con l'eccezione che si utilizza l'opzione /x anziché l'opzione /i. Per eseguire la disinstallazione dalle righe di comando è possibile anche includere l'opzione /quiet e altre opzioni standard. Se il pacchetto di Windows Installer di Generatore report (ReportBuilder3_x86.msi) è stato rimosso, non è possibile utilizzare facilmente la riga di comando per disinstallare Generatore report. Per ulteriori informazioni sulla procedura per rimuovere Generatore report tramite GUID, vedere la documentazione per il programma msiexec in MSDN Library.  
  
 Se le cartelle utilizzate da Generatore report includono file personalizzati, le cartelle e i file vengono conservati quando Generatore report viene rimosso. Vengono rimossi solo i file di Generatore report.  
  
### <a name="to-uninstall-report-builder-from-the-control-panel"></a>Per disinstallare Generatore report dal Pannello di controllo  
  
1.  Fare clic sul menu **Start** e scegliere **Pannello di controllo**.  
  
2.  Nel Pannello di controllo fare clic su **Programmi e caratteristiche**.  
  
3.  Individuare Generatore report di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nell'elenco **Nome** e fare clic sul nome del programma.  
  
4.  Fare clic su **Disinstalla**.  
  
5.  Se viene richiesto di confermare la disinstallazione di Generatore report, fare clic su **Sì**.  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>Per disinstallare Generatore report dalla riga di comando  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
2.  Nel **aperto** casella di testo, digitare `cmd.`  
  
3.  Nella finestra del prompt dei comandi, passare alla cartella contenente ReportBuilder3_x86.msi.  
  
4.  Digitare una riga di comando di base simile alla seguente:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 Per includere la registrazione, utilizzare una riga di comando simile alla seguente:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  Premere **INVIO**.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare, disinstallare e supporto di Generatore Report](../install-uninstall-and-report-builder-support.md)   
 [Installare la versione autonoma di Generatore Report &#40;Generatore Report&#41;](install-report-builder.md)  
  
  
