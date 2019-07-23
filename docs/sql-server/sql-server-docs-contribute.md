---
title: Come contribuire alla documentazione di SQL Server | Microsoft Docs
ms.date: 08/13/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: rothja
ms.author: jroth
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a13421707f332ee992d07daa4e9bd337996a7dad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136394"
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>Come contribuire alla documentazione di SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Chiunque può contribuire alla documentazione di SQL Server. Si può contribuire, ad esempio, correggendo gli errori tipografici, suggerendo spiegazioni più chiare e migliorando la precisione dal punto di vista tecnico. Questo articolo illustra come iniziare a contribuire al contenuto e come funziona il processo.

Si può contribuire alla documentazione usando due flussi di lavoro principali:

|||
|---|---|
| [Apportare modifiche nel browser](#githubui) | Adatto per piccole e rapide modifiche degli articoli. |
| [Apportare modifiche a livello locale con gli strumenti](#tools) | Adatto per modifiche più complesse, modifiche che interessano più articoli e contributi frequenti a docs.microsoft.com. |

Tutti i contenuti pubblici vengono convalidati dal team responsabile dei contenuti relativi a SQL per garantirne la coerenza e l'accuratezza tecnica. 

## <a id="githubui"></a> Apportare modifiche nel browser

È possibile apportare semplici modifiche al contenuto SQL Server nel browser e quindi inviarle a Microsoft. L'intera procedura è documentata nell'articolo [Panoramica della Guida per i collaboratori di Microsoft Docs](https://docs.microsoft.com/contribute/#quick-edits-to-existing-documents). Il video seguente illustra la procedura completa per l'invio delle modifiche nel browser:

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE23pxh]

> [!TIP]
> Si noti che la posizione del pulsante **Modifica** è leggermente diversa rispetto a quanto indicato nel video, ma la procedura è la stessa.
>
> ![Pulsante di modifica](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

## <a id="tools"></a> Apportare modifiche a livello locale con gli strumenti

Un'altra opzione di modifica è creare un fork del repository **sql-docs** o **azure-docs** e clonarlo nel computer locale. È quindi possibile usare un editor di Markdown e un client Git per inviare le modifiche. Questo flusso di lavoro è ottimale per le modifiche più complesse o che interessano più file. È ideale inoltre per i collaboratori che inviano spesso contributi a docs.microsoft.com.

Per contribuire con questo metodo, vedere gli articoli seguenti:

- [Creare un account GitHub](https://docs.microsoft.com/contribute/get-started-setup-github)
- [Installare gli strumenti di creazione del contenuto](https://docs.microsoft.com/contribute/get-started-setup-tools)
- [Configurare un repository Git locale](https://docs.microsoft.com/contribute/get-started-setup-local)
- [Usare gli strumenti per collaborare](https://docs.microsoft.com/contribute/how-to-write-workflows-major)

Se si invia una richiesta pull con modifiche significative alla documentazione, verrà visualizzato un commento in GitHub che richiede di inviare un **contratto di licenza per contributi (CLA)** online. È necessario completare il modulo online affinché la richiesta pull possa essere accettata.

## <a name="recognition"></a>Riconoscimento

Se le modifiche vengono accettate, l'utente viene riconosciuto come collaboratore all'inizio dell'articolo.

![Riconoscimento del contributo al contenuto](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>Panoramica di sql-docs

Questa sezione contiene informazioni aggiuntive sull'uso del repository **sql-docs**.

> [!IMPORTANT]
> Le informazioni di questa sezione sono specifiche per **sql-docs**. Se si modifica un articolo su SQL nella documentazione di Azure, vedere [il file Leggimi relativo al repository azure-docs su GitHub](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md).

Il repository [sql-docs](https://github.com/MicrosoftDocs/sql-docs) usa alcune cartelle standard per organizzare il contenuto.

| Cartella | Descrizione |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | Contiene tutto il contenuto pubblicato su SQL Server. Le diverse aree del contenuto sono organizzate logicamente in sottocartelle. |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | Contiene i file di inclusione. Questi file sono blocchi di contenuto che si possono includere in uno o più argomenti diversi. |
| **./media** | Ogni cartella può avere una sottocartella **media** per le immagini degli articoli. La cartella **media** a sua volta contiene sottocartelle con lo stesso nome degli argomenti in cui appare l'immagine. Le immagini devono essere file PNG con tutte le lettere minuscole e senza spazi. |
| **TOC.MD** | Un file di sommario. Ogni sottocartella può usare un file TOC.MD. |

#### <a name="applies-to-includes"></a>Inclusioni applies-to

Ogni articolo su SQL Server contiene un file di inclusione **applies-to** dopo il titolo. Indica a quali aree o versioni di SQL Server si riferisce l'articolo.

Si consideri l'esempio di Markdown seguente che esegue il pull nel file di inclusione **appliesto-ss-asdb-asdw-pdw-md.md**.

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

Questo comando aggiunge il testo seguente nella parte superiore dell'articolo:

![Testo applies-to](./media/sql-server-docs-contribute/applies-to.png)

Per trovare il file di inclusione applies-to corretto per l'articolo, usare i suggerimenti seguenti:

- Per un elenco delle inclusioni di uso comune, vedere [File di inclusione per il controllo delle versioni e Si applica a in SQL Server](applies-to-includes.md).
- Consultare un altro articolo che analizza la stessa funzionalità o un'attività correlata. Se si modifica quell'articolo, è possibile copiare il Markdown per il collegamento al file di inclusione applies-to (è possibile annullare la modifica senza inviarla).
- Cercare nella directory [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) i file che contengono il testo "applies-to". È possibile usare il pulsante **Find** in GitHub per filtrare rapidamente. Fare clic sul file per vedere come viene visualizzato.
- Prestare attenzione alla convenzione di denominazione. Se il nome contiene delle x, in genere sono segnaposto che indicano la mancanza di supporto per un servizio. Ad esempio, **appliesto-xx-xxxx-asdw-xxx-md.md** indica che esiste solo il supporto per Azure SQL Data Warehouse, poiché nel nome appare solo **asdw**, mentre gli altri campi contengono solo x.
- Alcune inclusioni specificano un numero di versione, ad esempio **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**. Usare questi file di inclusione solo quando si sa cha la funzionalità è stata introdotta con una versione specifica di SQL Server.

## <a name="contributor-resources"></a>Risorse per i collaboratori

- [Guida per il collaboratore per docs.microsoft.com](https://docs.microsoft.com/contribute/)
- [Guida di stile Microsoft](https://docs.microsoft.com/teamblog/style-guide)
- [Informazioni di base su Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> Per inviare commenti e suggerimenti relativi al prodotto anziché alla documentazione, [inserire qui eventuali suggerimenti per il prodotto SQL Server](https://feedback.azure.com/forums/908035-sql-server).

## <a name="next-steps"></a>Passaggi successivi

Esplorare il [repository sql-docs](https://github.com/MicrosoftDocs/sql-docs) su GitHub.

Trovare un articolo, inviare una modifica e collaborare con la community di SQL Server. 

Grazie.
