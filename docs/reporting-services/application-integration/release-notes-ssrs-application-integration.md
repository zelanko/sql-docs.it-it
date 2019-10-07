---
title: Note sulla versione per i controlli del Visualizzatore di report di SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923805"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Note sulla versione per i controlli Visualizzatore report per Web Form e WinForms di SSRS

Di seguito sono riportate le note sulla versione per i controlli Visualizzatore report di Web Form e WinForms, correlati a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Per le note sulla versione di SSRS, vedere [Note sulla versione per SQL Server Reporting Services (SSRS) 2017 e versioni successive](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzioni di bug | È stata ripristinata una modifica che ha rimosso gli assembly Microsoft. ReportViewer. Design dai riferimenti del progetto. |
|           | Come parte di altre modifiche, due assembly sono stati modificati dalla versione 15,0 alla versione 15,3. Questa operazione è stata ripristinata. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzioni di bug  | Anteprima di stampa corretta per il monitor DPI elevato |
|            | La finestra di dialogo stampa viene visualizzata al di fuori dello spazio visibile |
|            | Un numero elevato di parametri ha prodotto barre di scorrimento e elenchi a discesa di parametri non funzionanti correttamente |
|            | Correzione del problema relativo ai parametri null e di data e ora |
|            | Aggiornamento di JQuery alla versione 3.3.1 |
|            | Correzione della sovrapposizione con le celle della Tablix nel rendering HTML |
|            | Rimossi i riferimenti al progetto in fase di progettazione per eliminare gli assembly di Visual Studio non corretti aggiunti ai progetti |
|            | Correzione dell'accessibilità per la barra degli strumenti per la descrizione solo per gli elementi attivi |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| Descrizione della modifica | Dettagli |
| :----------------- | :------ |
| Correzione di un bug che impedisce il caricamento dei report senza parametri mediante **Server.LoadReportDefinition**. | &nbsp; |
| Controllo Visualizzatore report WebForms. | Supporta l'incorporamento nelle pagine da destra a sinistra (pagine che cambiano il flusso del testo usando la proprietà CSS *direction: rtl;* ).<br/><br/>Supporta la personalizzazione del testo della finestra di dialogo Stampa tramite l'interfaccia di localizzazione *IReportViewerMessages5*.<br/><br/>Migliorato il supporto dell'accessibilità.<br/><br/>pacchetto NuGet &bull; &nbsp; &nbsp; [per il controllo Visualizzatore di report di Web Form](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| Controllo Visualizzatore report WinForms. | Correzione della stampa quando un'app è in esecuzione in una modalità con valori DPI alti.<br/><br/>pacchetto NuGet &bull; &nbsp; &nbsp; [per il controllo Visualizzatore di report di WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Passaggi successivi

[Guida introduttiva](integrating-reporting-services-using-reportviewer-controls-get-started.md) ai controlli Visualizzatore report.

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
