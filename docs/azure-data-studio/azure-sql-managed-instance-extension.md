---
title: Estensione Istanza gestita di SQL di Azure
titleSuffix: Azure Data Studio
description: Usare Azure Data Studio con l'istanza gestita di SQL di Azure
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041136"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Supporto dell'istanza gestita per Azure Data Studio (anteprima)

Questa estensione consente di usare [Istanza gestita di SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) in [Azure Data Studio](https://github.com/Microsoft/azuredatastudio). L'estensione offre le funzionalità seguenti:

- Visualizzazione delle proprietà dell'istanza gestita (vCore, risorse di archiviazione usate).
- Monitoraggio dell'utilizzo della CPU e delle risorse di archiviazione nelle ultime due ore.
- Visualizzazione degli avvisi di configurazione e delle raccomandazioni di ottimizzazione.
- Visualizzazione dello stato delle repliche di database.
- Visualizzazione dei log degli errori filtrati.

## <a name="installations"></a>Installazioni

È possibile installare la versione ufficiale dell'estensione Istanza gestita seguendo la procedura descritta nella [documentazione di Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
Nel riquadro Estensioni cercare l'estensione "Istanza gestita" e installarla.  Si riceverà una notifica automatica degli aggiornamenti futuri dell'estensione.

Dopo aver installato l'estensione Istanza gestita, viene visualizzata una scheda `Managed Instance` in Azure Data Studio. La scheda include informazioni specifiche su Istanza gestita.

## <a name="properties"></a>Proprietà

Questa estensione consente di visualizzare le caratteristiche tecniche dell'istanza gestita e l'utilizzo di alcune risorse.

![Proprietà dell'istanza gestita](media/azure-sql-mi-extension/ads-mi-tab1.png)

Nel primo pannello sono visualizzati i dettagli seguenti:

- **Proprietà di base**, ad esempio numero disponibile di vCore, memoria, risorse di archiviazione, livello di servizio e generazione hardware e caratteristiche di I/O come velocità effettiva di scrittura del log dell'istanza o caratteristiche di I/O e velocità effettiva.
- **Utilizzo dell'unità SSD locale**. Al livello di servizio Utilizzo generico solo i file **TEMPDB** si trovano in locale, mentre al livello Business Critical tutti i file di database si trovano nell'unità SSD locale. In questa sezione è possibile visualizzare la quantità di spazio della risorsa di archiviazione locale usata da Istanza gestita.
- **Utilizzo dell'archiviazione Premium di Azure**: l'utente e il database di sistema al livello di servizio Utilizzo generico si trovano nell'archiviazione Premium di Azure. È possibile visualizzare la quantità di dati usati, lo spazio di archiviazione rimanente e il numero di file. Al livello di servizio Business Critical questa sezione è vuota.
- L'**Utilizzo risorse** visualizza l'archiviazione e la CPU usati dall'istanza nelle ultime due ore. Aumentare le dimensioni dell'istanza se si raggiunge il limite.

## <a name="recommendations"></a>Indicazioni

Questa estensione offre alcune raccomandazioni e alcuni avvisi che consentono di ottimizzare l'istanza gestita.

![Raccomandazioni sull'istanza gestita](media/azure-sql-mi-extension/ads-mi-tab2.png)

Nella tabella seguente sono riportate alcune delle raccomandazioni visualizzate:

- Raggiungimento del limite dello spazio di archiviazione: è necessario eliminare i dati non necessari o aumentare le dimensioni di archiviazione dell'istanza poiché i database che raggiungono il limite di archiviazione potrebbero non riuscire a elaborare le query di lettura.
- Raggiungimento del limite dell'istanza: se il caricamento avviene a ~22MB/s in GP oppure a ~48 MB/s in BC, Istanza gestita limita il caricamento per assicurare l'esecuzione dei backup.
- Utilizzo elevato di memoria: una bassa permanenza presunta delle pagine o la presenza di numerose statistiche di attesa `PAGEIOLATCH`potrebbero indicare che l'istanza sta eliminando le pagine dalla memoria e tentando continuamente di caricare più pagine dal disco.
- Limiti dei file di log: se i log raggiungono i [limiti di I/O al livello di servizio Utilizzo generico](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), potrebbe essere necessario aumentare le dimensioni del file per ottenere prestazioni migliori.
- Limiti dei file di log: se i log raggiungono i [limiti di I/O al livello di servizio Utilizzo generico](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), potrebbe essere necessario aumentare le dimensioni del file per ottenere prestazioni migliori. Questo problema potrebbe causare un utilizzo elevato della memoria e rallentare i backup.
- Problemi di disponibilità: un numero elevato di file di log virtuali può causare un impatto sulle prestazioni e un recupero di database potenzialmente più lungo al livello di servizio Utilizzo generico in caso di errore del processo.

È consigliabile rivedere regolarmente queste raccomandazioni, analizzare le cause radice e intraprendere azioni correttive. L'estensione Istanza gestita offre script che è possibile eseguire per attenuare alcuni dei problemi segnalati.

## <a name="replicas"></a>Repliche

L'estensione Istanza gestita consente di visualizzare lo stato delle repliche di database nell'istanza gestita.

![Repliche dell'istanza gestita](media/azure-sql-mi-extension/ads-mi-tab3.png)

Al livello di servizio Utilizzo generico, ogni database ha una sola replica (primaria), mentre nell'istanza Business Critical ogni database ha una replica primaria e tre repliche secondarie (una usata per i carichi di lavoro di sola lettura). È possibile monitorare il processo di sincronizzazione e verificare che tutte le repliche secondarie siano sincronizzate con la replica primaria.

## <a name="logs"></a>Log

L'estensione Istanza gestita visualizza le voci del log degli errori di SQL più rilevanti.

![Voci del log dell'istanza gestita](media/azure-sql-mi-extension/ads-mi-tab4.png)

Istanza gestita emette un numero elevato di voci di log, la maggior parte delle quali sono informazioni interne o di sistema. Alcune voci di log mostrano i nomi di database fisici (valori `GUID`) anziché i nomi di database logici effettivi.

L'estensione Istanza gestita esclude le voci di log non necessarie in base al [metodo Dimitri Furman](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506) e visualizza i nomi dei file logici effettivi anziché i nomi fisici.

## <a name="reporting-problems"></a>Segnalazione di problemi

Se si verificano problemi con l'estensione Istanza gestita, segnalare il problema nel [progetto GitHub dell'estensione](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues).

## <a name="maintainers"></a>Gestori

- [Jovan Popovic(MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>Codice di comportamento

Questo progetto ha adottato il [Codice di comportamento di Microsoft per l'open source][conduct-code].
Per altre informazioni, vedere le [Domande frequenti sul codice di comportamento][conduct-FAQ] o scrivere a [opencode@microsoft.com][conduct-email] per domande aggiuntive o commenti.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
