---
title: Che cos'è PolyBase? | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: 8d1c2cb27a2046f95ee250f16016488d30aa7929
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730307"
---
# <a name="what-is-polybase"></a>Che cos'è PolyBase?

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017 || >= aps-pdw-2016 || = azure-sqldw-latest"

PolyBase consente all'istanza di SQL Server 2016 di elaborare query Transact-SQL che leggono i dati da Hadoop. La stessa query può anche accedere a tabelle relazionali in SQL Server. PolyBase consente anche alla stessa query di creare un join per dati da Hadoop e SQL Server. In SQL Server, una [tabella esterna](../../t-sql/statements/create-external-table-transact-sql.md) oppure un'[origine dati esterna](../../t-sql/statements/create-external-data-source-transact-sql.md) fornisce la connessione a Hadoop.

![Logica PolyBase](../../relational-databases/polybase/media/polybase-logical.png "Logica PolyBase")

PolyBase esegue il push di alcuni calcoli sul nodo Hadoop per ottimizzare la query complessiva. Tuttavia, l'accesso esterno di PolyBase non è limitato a Hadoop. Sono supportate anche altre tabelle non relazionali non strutturate, ad esempio i file di testo delimitato.

> [!TIP]
> SQL Server 2019 CTP 2.0 introduce nuovi connettori per PolyBase, tra cui SQL Server, Oracle, Teradata e MongoDB. Per altre informazioni, vedere la [documentazione relativa a PolyBase per SQL Server 2019 CTP 2.0](polybase-guide.md?view=sql-server-ver15)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

PolyBase consente all'istanza di SQL Server di elaborare query Transact-SQL che leggono i dati da origini dati esterne. SQL Server 2016 e versioni successive possono accedere a dati esterni in Hadoop e Archiviazione BLOB di Azure. A partire da SQL Server 2019 CTP 2.0, è ora possibile usare PolyBase per accedere ai dati esterni in [SQL Server](polybase-configure-sql-server.md), [Oracle](polybase-configure-oracle.md), [Teradata](polybase-configure-teradata.md) e [MongoDB](polybase-configure-mongodb.md).

Le stesse query che accedono ai dati esterni possono essere anche destinate a tabelle relazionali nell'istanza di SQL Server. In questo modo è possibile combinare dati provenienti da origini esterne con dati relazionali di valore elevato nel database. In SQL Server, una [tabella esterna](../../t-sql/statements/create-external-table-transact-sql.md) oppure un'[origine dati esterna](../../t-sql/statements/create-external-data-source-transact-sql.md) fornisce la connessione a Hadoop.

PolyBase esegue il push di alcuni calcoli sul nodo Hadoop per ottimizzare la query complessiva. Tuttavia, l'accesso esterno di PolyBase non è limitato a Hadoop. Sono supportate anche altre tabelle non relazionali non strutturate, ad esempio i file di testo delimitato.

::: moniker-end

### <a name="supported-sql-products-and-services"></a>Prodotti e servizi SQL supportati

PolyBase offre queste stesse funzionalità per i prodotti SQL seguenti di Microsoft:

- SQL Server 2016 e versioni successive (solo Windows)
- Piattaforma di strumenti analitici (in precedenza Parallel Data Warehouse)
- Azure SQL Data Warehouse

### <a name="azure-integration"></a>Integrazione con Azure

Con il supporto sottostante di PolyBase, le query T-SQL possono anche importare ed esportare dati da Archiviazione BLOB di Azure. PolyBase consente inoltre ad Azure SQL Data Warehouse di importare ed esportare dati da Azure Data Lake Store e da Archiviazione BLOB di Azure.

## <a name="why-use-polybase"></a>Perché usare PolyBase

In passato era più difficile creare join tra i dati di SQL Server e dati esterni. Erano disponibili le due opzioni poco piacevoli seguenti:

- Trasferire la metà dei dati in modo che tutti i dati fossero in un formato o nell'altro.
- Eseguire query su entrambe le origini dati, quindi scrivere logica di query personalizzata per creare i join e integrare i dati a livello di client.

PolyBase consente di evitare queste spiacevoli opzioni usando T-SQL per creare join tra i dati.

In sostanza, PolyBase non richiede di installare software aggiuntivo nell'ambiente Hadoop. Si possono eseguire query sui dati esterni usando la stessa sintassi T-SQL usata per eseguire query su una tabella di database. Le azioni di supporto implementate da PolyBase vengono tutte eseguite in modo trasparente. L'autore della query non deve avere alcuna conoscenza di Hadoop.

### <a name="polybase-uses"></a>Usi di PolyBase

PolyBase rende possibili gli scenari seguenti in SQL Server:

- **Eseguire query sui dati archiviati in Hadoop da SQL Server o PDW.** Gli utenti scelgono di archiviare i dati in sistemi distribuiti e scalabili convenienti, come Hadoop. PolyBase semplifica la query dei dati con T-SQL.

- **Eseguire query sui dati archiviati in Archiviazione BLOB di Azure.** Nell'archivio BLOB di Azure è possibile salvare i dati da usare con i servizi di Azure.  PolyBase semplifica l'accesso ai dati con T-SQL.

- **Importare i dati da Hadoop, Archiviazione BLOB di Azure o Azure Data Lake Store.** Sfruttare la velocità della tecnologia columnstore e delle funzionalità di analisi di Microsoft SQL importando i dati da Hadoop, Archiviazione BLOB di Azure o Azure Data Lake Store in tabelle relazionali. Non è necessario uno strumento di importazione o ETL separato.

- **Esportare i dati in Hadoop, nell'archivio BLOB di Azure o in Azure Data Lake Store.** Archiviare i dati in Hadoop, nell'archivio BLOB di Azure o in Azure Data Lake Store per un'archiviazione conveniente e mantenerli online per accedervi facilmente.

- **Integrarsi con strumenti BI.** Usare PolyBase con la business intelligence e lo stack di analisi di Microsoft o usare strumenti di terze parti compatibili con SQL Server.

## <a name="performance"></a>Prestazioni

- **Eseguire il push del calcolo in Hadoop.** Query Optimizer prende una decisione basata sui costi di eseguire il push del calcolo in Hadoop se in questo modo migliorano le prestazioni della query.  Per prendere la decisione basata sui costi, usa le statistiche sulle tabelle esterne. Il push del calcolo crea processi MapReduce e sfrutta le risorse di calcolo distribuite di Hadoop.

- **Ridimensionare le risorse di calcolo.** Per migliorare le prestazioni delle query, è possibile usare i [gruppi con scalabilità orizzontale di PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)per SQL Server. In questo modo viene abilitato il trasferimento dei dati paralleli tra le istanze di SQL Server e i nodi di Hadoop e vengono aggiunte le risorse di calcolo per operare sui dati esterni.

<!--SQL Server 2016/2017-->
::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="next-steps"></a>Passaggi successivi

Prima di usare PolyBase, è necessario [installare la funzionalità PolyBase](polybase-installation.md). Vedere quindi le guide di configurazione seguenti a seconda dell'origine dati:

- [Hadoop](polybase-configure-hadoop.md)
- [Archiviazione BLOB di Azure](polybase-configure-azure-blob-storage.md)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15||>= sql-server-ver15||=sqlallproducts-allversions"

## <a name="next-steps"></a>Passaggi successivi

Prima di usare PolyBase, è necessario [installare la funzionalità PolyBase](polybase-installation.md). Vedere quindi le guide di configurazione seguenti a seconda dell'origine dati:
- [Hadoop](polybase-configure-hadoop.md)
- [Archiviazione BLOB di Azure](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [Tipi generici ODBC](../../relational-databases/polybase/polybase-installation.md)

::: moniker-end
