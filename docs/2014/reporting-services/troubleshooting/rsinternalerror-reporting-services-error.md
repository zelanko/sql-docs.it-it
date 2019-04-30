---
title: rsInternalError - Errore di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fbdb1c9e8df7ec3223dc4050f9dd6f83c56152d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228981"
---
# <a name="rsinternalerror---reporting-services-error"></a>rsInternalError - Errore di Reporting Services
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|rsInternalError|  
|Origine evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Testo del messaggio|Errore interno nel server di report. Per altre informazioni, vedere il log degli errori.|  
  
## <a name="explanation"></a>Spiegazione  
 Si tratta di un messaggio di errore generico, spesso seguito da un errore più descrittivo che include ulteriori dettagli.  
  
 Gli errori interni non sono comuni. Se viene visualizzato questo errore, nei log di traccia del server di report sono disponibili ulteriori informazioni. Se inoltre si esegue il servizio come amministratore locale nello stesso computer in cui si è verificato l'errore, è possibile visualizzare lo stack di chiamate per ottenere ulteriori informazioni.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per stabilire la causa specifica di questo messaggio, esaminare i file di log del server di report, disponibili in \Microsoft SQL Server\MSRS12.\<nomeistanza >\Reporting Services\LogFiles. Per altre informazioni, vedere [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
 Per visualizzare lo stack di chiamate, fare clic con il pulsante destro del mouse nella pagina in cui si è verificato l'errore e scegliere **Visualizza origine**. Per visualizzare lo stack di chiamate, è necessario disporre delle autorizzazioni di amministratore nello stesso computer in cui si verifica l'errore.  
  
 Se non sono disponibili informazioni aggiuntive, è possibile riprovare a eseguire la richiesta.  
  
## <a name="internal-only"></a>Solo interno  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare e arrestare il servizio del server di report](../report-server/start-and-stop-the-report-server-service.md)  
  
  
