---
title: Estensione Kusto (KQL) per Azure Data Studio
description: Questo articolo descrive come connettersi ed eseguire query sui cluster di Esplora dati di Azure con Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 2ffe3945f8dd7e8c0ce9cf504c09622ca1a20331
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725190"
---
# <a name="kusto-kql-extension-for-azure-data-studio-preview"></a>Estensione Kusto (KQL) per Azure Data Studio (anteprima)

L'estensione Kusto (KQL) per [Azure Data Studio](../what-is.md) consente di connettersi ed eseguire query nei cluster di [Esplora dati di Azure](/azure/data-explorer/data-explorer-overview).

Gli utenti possono scrivere ed eseguire query KQL e creare notebook con il [kernel Kusto](../notebooks/notebooks-kusto-kernel.md) provvisto di IntelliSense.

L'abilitazione dell'esperienza Kusto (KQL) nativa in Azure Data Studio consente a data engineer, data scientist e analisti dei dati di osservare rapidamente tendenze e anomalie in grandi quantità di dati archiviati in Esplora dati di Azure.

Questa estensione è attualmente disponibile in anteprima.

## <a name="prerequisites"></a>Prerequisiti

Se non si ha una sottoscrizione di Azure, creare un [account Azure gratuito](https://azure.microsoft.com/free/) prima di iniziare.

Sono richiesti anche i prerequisiti seguenti:

- [Azure Data Studio installato](../download-azure-data-studio.md).
- [Un cluster e un database di Esplora dati di Azure](/azure/data-explorer/create-cluster-database-portal).

## <a name="install-the-kusto-kql-extension"></a>Installare l'estensione Kusto (KQL)

Per installare l'estensione Kusto (KQL) in Azure Data Studio, seguire questa procedura.

1. Aprire Gestione estensioni in Azure Data Studio. È possibile selezionare l'icona delle estensioni o scegliere **Estensioni** dal menu Visualizza.

2. Digitare *Kusto* nella barra di ricerca.

3. Selezionare l'estensione **Kusto (KQL)** e visualizzarne i dettagli.

4. Selezionare **Installa**.

:::image type="content" source="media/kusto-extension/kusto-extension-icon.png" alt-text="Estensione Kusto":::

## <a name="how-to-connect-to-an-azure-data-explorer-cluster"></a>Come connettersi a un cluster di Esplora dati di Azure

### <a name="find-your-azure-data-explorer-cluster"></a>Trovare il cluster di Esplora dati di Azure

Trovare il cluster di Esplora dati di Azure nel [portale di Azure](https://ms.portal.azure.com/#home), quindi trovare l'URI del cluster.

:::image type="content" source="media/kusto-extension/kusto-extension-adx-cluster-uri.png" alt-text="Estensione Kusto":::

È possibile iniziare immediatamente usando il cluster *help.kusto.windows.net*.

Gli esempi di questo articolo usano i dati del cluster help.kusto.windows.net.

### <a name="connection-details"></a>Dettagli connessione

Per configurare un cluster di Esplora dati di Azure per la connessione, seguire questa procedura.

1. Selezionare **Nuova connessione** nel riquadro **Connessioni**.

2. Immettere i dati necessari in **Dettagli connessione**.
    1. In **Tipo di connessione** selezionare *Kusto*.
    2. In **Cluster** immettere il cluster di Esplora dati di Azure.

        > [!Note]
        > Immettere il nome del cluster senza includere il prefisso `https://` o accodare `/`.

    3. In **Tipo di autenticazione** usare l'impostazione predefinita *Azure Active Directory - Universale con supporto MFA*.
    4. In **Account** usare le informazioni dell'account.
    5. In **Database** usare *Predefinito*.
    6. In **Gruppo di server** usare *Predefinito*.
        1. È possibile usare questo campo per organizzare i server in un gruppo specifico.
    7. Lasciare vuoto il campo **Nome (facoltativo)** .
        1. È possibile usare questo campo per assegnare un alias al server.

    :::image type="content" source="media/kusto-extension/kusto-extension-connection-details.png" alt-text="Estensione Kusto":::

## <a name="how-to-query-an-azure-data-explorer-database-in-azure-data-studio"></a>Come eseguire query in un database di Esplora dati in Azure Data Studio

Ora che è stata configurata una connessione al cluster Esplora dati di Azure, è possibile eseguire una query sui database usando Kusto (KQL).

Per creare una nuova scheda query è possibile selezionare **File > nuova query**, usare *CTRL+N* oppure fare clic con il pulsante destro del mouse sul database e selezionare **Nuova query**.

Quando viene aperta la scheda della nuova query, immettere la query Kusto.

Di seguito sono riportati alcuni esempi di query KQL:

```kusto
StormEvents
| limit 1000
```

```kusto
StormEvents
| where EventType == "Waterspout"
```

Per altre informazioni sulla scrittura di query KQL, vedere [Scrivere query per Esplora dati di Azure](/azure/data-explorer/write-queries#overview-of-the-query-language)

## <a name="view-extension-settings"></a>Visualizzare le impostazioni dell'estensione

Per modificare le impostazioni per l'estensione Kusto, seguire questa procedura.

1. Aprire Gestione estensioni in Azure Data Studio. È possibile selezionare l'icona delle estensioni o scegliere **Estensioni** dal menu Visualizza.

2. Trovare l'estensione **Kusto (KQL)** .

3. Selezionare l'icona **Gestisci**.

4. Selezionare l'icona **Impostazioni estensione**.

Le impostazioni delle estensioni hanno un aspetto simile al seguente:

:::image type="content" source="media/kusto-extension/kusto-extension-settings.png" alt-text="Estensione Kusto":::

## <a name="sanddance-visualization"></a>Visualizzazione SandDance

L'[estensione SandDance](../sanddance-extension.md) e l'estensione Kusto (KQL) usate insieme in Azure Data Studio apportano una visualizzazione interattiva avanzata. Nel set di risultati della query KQL selezionare il pulsante **Visualizzatore** per avviare [SandDance](https://sanddance.js.org/).

:::image type="content" source="media/kusto-extension/kusto-extension-sanddance-demo.gif" alt-text="Estensione Kusto":::

## <a name="known-issues"></a>Problemi noti

| Dettagli | Soluzione alternativa |
|---------|------------|
| [Il viewlet di connessione Kusto dopo il ricaricamento non funziona](https://github.com/microsoft/azuredatastudio/issues/12475). | N/D |
| [Non è possibile riconnettersi automaticamente](https://github.com/microsoft/azuredatastudio/issues/11830). | Disconnettersi e riconnettersi al cluster di Esplora dati di Azure. |
| [L'aggiornamento del cluster Kusto non sembra riconnettersi correttamente](https://github.com/microsoft/azuredatastudio/issues/11824). | Disconnettersi e riconnettersi al cluster di Esplora dati di Azure. |
| [La connessione a un cluster dovrebbe visualizzare il dashboard del cluster anziché il database](https://github.com/microsoft/azuredatastudio/issues/12549) | N/D |
| Per ogni tabella nel database del cluster di dati di Azure, è disponibile solo l'opzione **SELECT TOP 1000** anziché **TAKE 10**. | N/D |

È possibile inviare una [richiesta di funzionalità](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=) per inviare commenti e suggerimenti al team del prodotto.  
È possibile registrare un [bug](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=) per fornire commenti e suggerimenti al team del prodotto.

## <a name="next-steps"></a>Passaggi successivi

- [Creare ed eseguire un notebook Kusto](../notebooks/notebooks-kusto-kernel.md)
- [Notebook Kqlmagic in Azure Data Studio](../notebooks/notebooks-kqlmagic.md)
- [Scheda di riferimento rapido sul passaggio da SQL a Kusto](/azure/data-explorer/kusto/query/sqlcheatsheet)
- [Informazioni su Esplora dati di Azure](/azure/data-explorer/data-explorer-overview)
- [Uso delle visualizzazioni SandDance](https://sanddance.js.org/)
