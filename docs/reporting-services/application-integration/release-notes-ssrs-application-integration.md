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
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730902"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Note sulla versione per i controlli visualizzatore Report per Web Form e Windows Form di SSRS

Queste sono le note sulla versione per i controlli visualizzatore Report di Web Form e Windows Form, correlati [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Per le note sulla versione per SSRS, vedere [note sulla versione per SQL Server Reporting Services (SSRS) 2017 e versioni successive](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzioni di bug | Ripristinare una modifica che rimossi gli assembly Microsoft.ReportViewer.Design da riferimenti del progetto. |
|           | Come parte di altre modifiche, due assembly sono stati modificati dalla versione 15.0 per versione 15.3. Questo è stato ripristinato. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzioni di bug  | Anteprima di stampa appropriato per valori DPI alti monitoraggio |
|            | Finestra di dialogo Stampa mostrerebbe esterno dello spazio visibile |
|            | Ha restituito un numero elevato di parametri di elenchi a discesa non funziona correttamente e le barre di scorrimento di parametro |
|            | Risolto un problema con i parametri ora Null e la data |
|            | JQuery aggiornato alla versione 3.3.1 |
|            | Risolto la sovrapposizione con le celle della tablix nel rendering HTML |
|            | Rimuovere la fase di progettazione progetto fa riferimento a eliminare gli assembly di Visual Studio non corretti da aggiungere ai progetti |
|            | Correzione di accessibilità per la barra degli strumenti raccontare una storia solo per gli elementi attivi |
| &nbsp; | &nbsp; |

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
