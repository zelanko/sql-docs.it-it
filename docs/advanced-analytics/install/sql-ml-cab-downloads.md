---
title: Download CAB per SQL Server aggiornamenti cumulativi
description: Download di pacchetti e CAB r e Python per SQL Server Machine Learning Services e SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7b77a1fd3a0d2575f0add7badb1c5bf632d29d70
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715837"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Download CAB per aggiornamenti cumulativi di SQL Server istanze di analisi nel database

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server le istanze configurate per l'analisi nel database includono funzionalità di R e Python. Queste funzionalità vengono fornite nei file CAB, installate e gestite tramite SQL Server installazione. Nei dispositivi connessi a Internet, gli aggiornamenti CAB vengono in genere applicati tramite Windows Update. Nei server disconnessi è necessario scaricare e applicare manualmente i file CAB. 

Questo articolo fornisce i collegamenti di download ai file CAB per ogni aggiornamento cumulativo. Per altre informazioni sulle installazioni offline, vedere [Install SQL Server machine learning Components without Internet Access](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Prerequisiti

Iniziare con un'installazione di base.

+ In SQL Server Machine Learning Services, la versione iniziale è l'installazione di base. 
+ In SQL Server 2016 R Services, è possibile iniziare con la versione iniziale, SP1 o SP2. 

È anche possibile applicare aggiornamenti cumulativi a un server autonomo.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CAB

I file CAB sono elencati in ordine cronologico inverso. Quando si scaricano i file CAB e li si trasferiscono nel computer di destinazione, inserirli in una cartella pratica, ad esempio **download** , oppure la cartella% Temp% dell'utente di installazione.

|Versione  |Componente | Collegamento di download  | Problemi risolti | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| I file binari all'interno del pacchetto sono ora firmati. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| I file binari all'interno del pacchetto sono ora firmati. |
| | Microsoft Python aperto     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| I file binari all'interno del pacchetto sono ora firmati. |
| | Server Python    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| I file binari all'interno del pacchetto sono ora firmati.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contiene una correzione per l'aggiornamento di un [R server autonomo operativo](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), come installato tramite SQL Server installazione. Usare i CAB CU13 e seguire [queste istruzioni](sql-machine-learning-standalone-windows-install.md#apply-cu) per applicare l'aggiornamento. |
| | Microsoft Python aperto     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contiene una correzione per l'aggiornamento di un [Server Python autonomo operativo](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), come installato tramite SQL Server installazione. Usare i CAB CU13 e seguire [queste istruzioni](sql-machine-learning-standalone-windows-install.md#apply-cu) per applicare l'aggiornamento. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correzioni minori.|
| | Microsoft Python aperto     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Quando vengono rimossi i duplicati, Python rx_data_step perde l'ordine delle righe. <br/>SPEE non riesce a rilevare il tipo di dati nell'indice columnstore cluster. <br/>Restituisce una tabella vuota quando le colonne contengono tutti i valori null. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python aperto     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python aperto     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipi di dati DateTime nella query SPEES.<br/>messaggi di errore migliorati in microsoftml quando mancano modelli con training preliminare.<br/> Corregge le variabili e le funzioni di trasformazione revoscalepy.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Errori relativi al percorso lungo in rxInstallPackages.<br/>Connessioni in un loopback per RxExec.
| | Microsoft Python aperto    | Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Connessioni in un loopback per rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python aperto     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| |  Server Python    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python aperto     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. |
| | Server Python    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Serializzazione del modello Python in revoscalepy, tramite la [funzione rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>Supporto dei [punteggi nativi](../sql-native-scoring.md) , oltre ai miglioramenti apportati al [punteggio in tempo reale](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Non sono state apportate modifiche alle versioni precedenti. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python aperto     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Non sono state apportate modifiche alle versioni precedenti. | 
| | Server Python    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Aggiunge rx_create_col_info per restituire le informazioni sullo schema. <br/>Miglioramenti apportati a [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) per supportare scenari paralleli usando il `RxLocalParallel` contesto di calcolo.|
|**Versione iniziale** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python aperto     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Server Python    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CAB

Per SQL Server 2016 R Services, le versioni di base sono la versione RTM o una versione Service Pack.

|Versione  |Collegamento di download  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> Quando si installa SQL Server 2016 SP1 CU4 o SP1 CU5 offline, scaricare SRO_ 3.2.2.16000 _1033. cab. Se è stato scaricato SRO_ 3.2.2.13000 _1033. cab da FWLINK 831785 come indicato nella finestra di dialogo del programma di installazione, rinominare il file come SRO_ 3.2.2.16000 _1033. cab prima di installare l'aggiornamento cumulativo.

Se si vuole visualizzare il codice sorgente per Microsoft R, è disponibile per il download come archivio in formato. tar: [Scarica R Server programmi di installazione](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

[Applicare gli aggiornamenti cumulativi nei computer senza accesso a Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Applicare gli aggiornamenti cumulativi nei computer con connettività Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Applicare gli aggiornamenti cumulativi a un server autonomo](sql-machine-learning-standalone-windows-install.md#apply-cu)
