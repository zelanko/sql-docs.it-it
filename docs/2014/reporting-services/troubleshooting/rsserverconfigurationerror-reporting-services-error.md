---
title: rsServerConfigurationError - Errore di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a5b89e0e1a9034327e531eda8dd4e1c68997bc9f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59966887"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Errore di Reporting Services
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|rsServerConfiguration|  
|Origine evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Testo del messaggio|Il server di report ha rilevato un errore di configurazione.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore è generico e si verifica quando le impostazioni di configurazione del server di report o di uno strumento di creazione dei report non sono valide. All'errore è generalmente associato un secondo messaggio che indica la causa effettiva dell'errore stesso.  
  
 Nell'elenco seguente vengono riepilogate le possibili cause:  
  
-   Il file RSReportServer.config o RSReportDesigner.config non può essere trovato o letto.  
  
-   Gli elementi XML nel file di configurazione mancano o non sono validi.  
  
-   I valori per uno o più elementi XML mancano o non sono validi.  
  
-   Le impostazioni del Registro di sistema non sono valide.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se questo errore inizia a verificarsi dopo che il file di configurazione è stato modificato manualmente, rimuovere le modifiche e immettere il valore precedente o ripristinare una versione precedente se è disponibile un backup.  
  
 Per rivedere informazioni sul messaggio di errore aggiuntive che accompagna il `rsServerConfiguration` errori, esaminare i report server trace log file, che si trovano in \Microsoft SQL Server\MSRS12.\< NomeIstanza > Services\LogFiles. Per altre informazioni, vedere [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="internal-only"></a>Solo interno  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione di Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
