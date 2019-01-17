---
title: Virtualizzare i dati esterni in SQL Server 2019 CTP 2.0 | Microsoft Docs
description: Questa pagina illustra i passaggi per l'uso della procedura guidata di creazione di una tabella esterna per le origini dati relazionali
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a8f5f55dfa0a569ec88542f819e30d21889997e3
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596672"
---
# <a name="use-the-external-table-wizard-with-relational-data-sources"></a>Usare la procedura guidata Tabella esterna con origini dati relazionali

Uno degli scenari chiave per SQL Server 2019 CTP 2.0 è la possibilità di virtualizzare i dati. Questo processo consente di mantenere i dati nella posizione originale. È possibile *virtualizzare* i dati in un'istanza di SQL Server in modo da poter eseguire query nella versione virtualizzata come in qualsiasi altra tabella in SQL Server. Questo processo riduce al minimo la necessità di ricorrere a processi ETL (estrazione, trasformazione e caricamento). Per eseguire il processo è necessario l'uso di connettori Polybase. Per altre informazioni sulla virtualizzazione dei dati, vedere [Get started with PolyBase](polybase-guide.md) (Introduzione a PolyBase).

## <a name="start-the-external-table-wizard"></a>Avviare la procedura guidata Tabella esterna

Connettersi all'istanza master usando l'indirizzo IP/numero di porta (31433) ottenuti alla fine dello script di distribuzione. Espandere il nodo **Database** in Esplora oggetti. Selezionare quindi uno dei database di cui si vogliono virtualizzare i dati da un'istanza di SQL Server esistente. Fare clic con il pulsante destro del mouse sul database e selezionare **Create External Table** (Crea tabella esterna) per avviare la procedura guidata Virtualize Data (Virtualizza dati). È anche possibile avviare la procedura guidata Virtualize Data (Virtualizza dati) dal riquadro comandi. Premere CTRL+MAIUSC+P in Windows o Cmd+MAIUSC+P in un computer Mac.

![Procedura guidata Virtualize Data (Virtualizza dati)](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>Selezione un'origine dati

Se è stata avviata la procedura guidata da uno dei database, la casella di riepilogo a discesa di destinazione viene compilata automaticamente. In questa pagina è anche possibile immettere o modificare il database di destinazione. I tipi di origini dati esterne supportati dalla procedura guidata sono SQL Server e Oracle.

> [!NOTE]
>SQL Server è evidenziato per impostazione predefinita.


![Selezione un'origine dati](media/data-virtualization/select-data-source.png)

Selezionare **Avanti** per continuare.

## <a name="create-a-database-master-key"></a>Creare una chiave master del database

In questo passaggio verrà creata una chiave master del database. La creazione di una chiave master è obbligatoria. La chiave master protegge le credenziali usate da un'origine dati esterna. Scegliere una password complessa per la chiave master. Eseguire anche un backup della chiave master usando **BACKUP MASTER KEY**. Archiviare il backup in una posizione esterna protetta.

![Creare una chiave master del database](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> Se si ha già una chiave master del database, i campi di input sono limitati ed è possibile ignorare questo passaggio. Selezionare **Avanti** per continuare.

> [!NOTE]
> Se non si sceglie una password complessa, la procedura guidata esegue l'operazione nell'ultimo passaggio. Questo è un problema noto

## <a name="enter-external-data-source-credentials"></a>Immettere le credenziali dell'origine dati esterna

In questo passaggio immettere i dettagli dell'origine dati esterna e delle credenziali per creare un oggetto origine dati esterna. Le credenziali vengono usate per la connessione dell'oggetto di database all'origine dati. Immettere un nome per l'origine dati esterna. Immettere ad esempio il nome Test. Specificare i dettagli di connessione di SQL Server dell'origine dati esterna. Immettere il **Nome server** e il **Nome database** in cui si vuole creare l'origine dati esterna.

Il passaggio successivo consiste nel configurare le credenziali. Immettere un nome per le credenziali. Il nome corrisponde alle credenziali con ambito database usate per archiviare in modo sicuro le informazioni di accesso per l'origine dati esterna creata. Immettere ad esempio il nome TestCred. Immettere un nome utente e una password per la connessione all'origine dati.

![Credenziali dell'origine dati esterna](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>Mapping della tabella dati esterna

Nella pagina successiva selezionare le tabelle per cui si vuole creare viste esterne. Quando si selezionano database principali, vengono incluse anche le tabelle figlio. Dopo aver selezionato le tabelle, viene visualizzata una tabella di mapping a destra. Nella tabella è possibile apportare modifiche ai tipi. È anche possibile modificare il nome della tabella esterna selezionata.

![Credenziali dell'origine dati esterna](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>Per modificare la vista di mapping, fare doppio clic su un altra tabella selezionata.

> [!IMPORTANT]
>Il tipo foto non è supportato dallo strumento Tabella esterna. Se si crea una vista esterna con un tipo foto, viene visualizzato un errore dopo aver creato la tabella. La tabella viene comunque creata.

## <a name="summary"></a>Riepilogo

Questo passaggio visualizza un riepilogo delle selezioni. Indica il nome delle credenziali con ambito database e gli oggetti origine dati esterna creati nel database di destinazione. Selezionare **Genera script** per creare lo script in T-SQL, la sintassi usata per creare l'origine dati esterna. Selezionare **Crea** per creare l'oggetto origine dati esterna.

![Schermata Riepilogo](media/data-virtualization/virtualize-data-summary.png)

Se si seleziona **Crea**, viene visualizzato l'oggetto origine dati esterna creato nel database di destinazione.

![Origini dati esterne](media/data-virtualization/external-data-sources.png)

Se si seleziona **Genera script**, viene visualizzata la query T-SQL generata per creare l'oggetto origine dati esterna.

![Genera script](media/data-virtualization/generated-script.png)

> [!NOTE]
> Il pulsante **Genera script** deve essere visibile solo nell'ultima pagina della procedura guidata. Attualmente viene visualizzato in tutte le pagine.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data di SQL Server e gli scenari correlati, vedere [Che cos'è un cluster Big Data di SQL Server?](../../big-data-cluster/big-data-cluster-overview.md)
