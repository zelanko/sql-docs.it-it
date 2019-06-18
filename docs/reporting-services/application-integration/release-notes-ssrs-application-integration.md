---
title: Note sulla versione per i controlli del Visualizzatore di report di SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6d4da6d5574288fa66ea18a9c63b1488a6abcca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225997"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Note sulla versione per i controlli visualizzatore Report per Web Form e Windows Form di SSRS

Queste sono le note sulla versione per i controlli visualizzatore Report di Web Form e Windows Form, correlati [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Per le note sulla versione per SSRS, vedere [note sulla versione per SQL Server Reporting Services (SSRS) 2017 e versioni successive](../release-notes-reporting-services.md).

## <a name="15900148"></a>15.900.148

| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzione di un bug che impedisce il caricamento dei report senza parametri mediante **Server.LoadReportDefinition**. | &nbsp; |
| Controllo Visualizzatore report WebForms. | Supporta l'incorporamento nelle pagine da destra a sinistra (pagine che cambiano il flusso del testo usando la proprietà CSS *direction: rtl;* ).<br/><br/>Supporta la personalizzazione del testo della finestra di dialogo Stampa tramite l'interfaccia di localizzazione *IReportViewerMessages5*.<br/><br/>Migliorato il supporto dell'accessibilità.<br/><br/>&bull; &nbsp; &nbsp; [Pacchetto NuGet per il controllo Visualizzatore Report di Web Form](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| Controllo Visualizzatore report WinForms. | Correzione della stampa quando un'app è in esecuzione in una modalità con valori DPI alti.<br/><br/>&bull; &nbsp; &nbsp; [Pacchetto NuGet per il controllo Visualizzatore Report di Windows Form](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Passaggi successivi

[Guida introduttiva](integrating-reporting-services-using-reportviewer-controls-get-started.md) ai controlli Visualizzatore report.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
