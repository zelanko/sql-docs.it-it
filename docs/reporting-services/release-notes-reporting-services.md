---
title: Note sulla versione di (SSRS) 2017 e versioni successive | Microsoft Docs
ms.date: 09/01/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maghan
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: c85d3811fc467d94dc1841b871964e3bb594e2df
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283294"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Note sulla versione per SQL Server Reporting Services (SSRS) 2017 e versioni successive

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

Questo articolo descrive le modifiche in [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS), per le versioni 2017 e versioni successive.

Per le note sulla versione per i controlli visualizzatore Report, vedere [note sulla versione per il Visualizzatore Report di controlli per Web Form e Windows Form di SSRS](application-integration/release-notes-ssrs-application-integration.md).

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->

## <a name="1406001109-20190212"></a>14.0.600.1109, 12/02/2019

| Risolto un problema | Dettagli |
| :---------- | :------ |
| Le pianificazioni degli snapshot dei report di cache diventano "Pianificazione in base al report" dopo la modifica della sottoscrizione. | &nbsp; |
| rc:Toolbar=false non funziona nell'edizione Express. | &nbsp; |
| Non viene eseguito correttamente il rendering di alcuni caratteri thai durante l'esportazione di report impaginati in formato PDF. | &nbsp; |
| Si verifica un deadlock durante la notifica del completamento di sottoscrizioni guidate dai dati. | &nbsp; |
| In alcune circostanze, le immagini incorporate non vengono visualizzate quando viene usato il parametro rc:Toolbar=False. | &nbsp; |
| Non è possibile creare sottoscrizioni guidate dai dati per report che usano parametri a cascata. | &nbsp; |
| Non è possibile modificare le sottoscrizioni configurate con un intervallo non valido. | &nbsp; |
| Aggiornamenti per la sicurezza. | &nbsp; |
| Non viene visualizzata l'interfaccia utente dei report collegati. | &nbsp; |
| Alcuni report impaginati con controlli di un'area dati Tablix annidata hanno tipi di carattere non corretti. | &nbsp; |
| Spazi vuoti in modo non corretto viene aggiunto a determinati report impaginati che contengono aree dati tablix. | &nbsp; |
| Le righe di intestazione spariscono quando si espandono le griglie dati semplici di report per dispositivi mobili. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 12/09/2018

È stato corretto il problema seguente:

| Risolto un problema | Dettagli |
| :---------- | :------ |
| L'autenticazione personalizzata non restituisce informazioni sui cookie corrette. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 31/08/2018

| Risolto un problema | Dettagli |
| :---------- | :------ |
| La presenza di una casella di testo all'interno di un rettangolo impedisce l'ingrandimento in verticale del rettangolo quando rc:Toolbar=False e contiene testo lungo. | &nbsp; |
| Le dimensioni del testo non vengono adattate se pageHeight è minore di 0,5 pollici. | &nbsp; |
| Un deadlock si verifica nel database del catalogo SSRS quando viene usato con CRM. | &nbsp; |
| Le intestazioni di colonna con allineamento verticale non vengono visualizzate correttamente quando si scorre verso il basso nel report. | &nbsp; |
| Per gli utenti aggiunti al ruolo SCOM Reporting verrà bloccato l'accesso al portale Web SSRS. | &nbsp; |
| Caratteri tailandese non viene esportata correttamente nel PDF. | &nbsp; |
| Modifica del comportamento del ruolo browser. | &nbsp; |
| rc:Toolbar=false non funziona nell'edizione Express. | &nbsp; |
| Manca la barra di scorrimento verticale nell'area dei messaggi di richiesta dei parametri. | &nbsp; |
| Aggiornamento del runtime per i report per dispositivi mobili. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 25/04/2018

| Risolto un problema | Dettagli |
| :---------- | :------ |
| La pagina Sottoscrizione guidata dai dati non visualizza l'opzione di recapito dopo la creazione. | &nbsp; |
| Se si esegue l'aggiornamento da SSRS 2012 a SSRS 2017, RSManagement genererà un'eccezione a intervalli di pochi secondi. | &nbsp; |
| Non è possibile modificare i valori predefiniti per i parametri multivalore in IE11. | &nbsp; |
| Le pianificazioni sono vuote quando viene eseguita una pianificazione condivisa. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 28/02/2018

| Risolto un problema | Dettagli |
| :---------- | :------ |
| La visibilità di Parametro report in un report collegato viene ripristinata dopo la modifica delle relative proprietà. | &nbsp; |
| Il parametro URL rc:Toolbar=false non funziona nell'edizione Express. | &nbsp; |
| Le espressioni in una casella di testo con la proprietà CanGrow impostata su false risultati nei valori non vengono visualizzati. | &nbsp; |
| Aggiunta del collegamento _Ulteriori informazioni_ per il codice Product Key nel programma di installazione. | &nbsp; |
| Il portale Web con autenticazione basata su form personalizzata ignora il cookie di scadenza variabile. | &nbsp; |
| L'esportazione in Word crea altezze di righe non uniformi se il contenuto della riga è vuoto. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 09/01/2018

Sono stati implementati alcuni aggiornamenti della sicurezza.

### <a name="140600490-20171101"></a>14.0.600.490, 01/11/2017

Problemi risolti con l'aggiornamento dello SKU.

## <a name="140600451-20170930"></a>14.0.600.451, 30/09/2017

Versione iniziale.

## <a name="next-steps"></a>Passaggi successivi

[Novità di Reporting Services (SSRS)](what-s-new-in-sql-server-reporting-services-ssrs.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
