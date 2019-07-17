---
title: Installazione di ricerca Full-Text SQL Server in Linux
description: Questo articolo descrive come installare la ricerca full-text di SQL Server in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 9a637e6b12c674102bd09239739a137e1d442e12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065088"
---
# <a name="install-sql-server-full-text-search-on-linux"></a>Installazione di ricerca Full-Text SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

La procedura seguente installa [ricerca Full-Text di SQL Server](../relational-databases/search/full-text-search.md) (**mssql-server-fts**) in Linux. Ricerca full-Text consente di eseguire query full-text su dati di tipo carattere in tabelle di SQL Server. Per problemi noti per questa versione, vedere la [note sulla versione](sql-server-linux-release-notes.md).

> [!NOTE]
> Prima di installare ricerca Full-Text di SQL Server, prima di tutto [installare SQL Server](sql-server-linux-setup.md#platforms). Ciò consente di configurare le chiavi e i repository che usano quando si installa il **mssql-server-fts** pacchetto.

Installare ricerca Full-Text di SQL Server per la tua piattaforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Eseguire l'installazione in RHEL</a>

Usare i comandi seguenti per installare il **mssql-server-fts** in Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-fts
```

Se hai già **mssql-server-fts** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

Se è necessaria un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Eseguire l'installazione in Ubuntu</a>

Usare i comandi seguenti per installare il **mssql-server-fts** in Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

Se hai già **mssql-server-fts** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

Se è necessaria un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Eseguire l'installazione in SLES</a>

Usare i comandi seguenti per installare il **mssql-server-fts** su SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-fts
```

Se hai già **mssql-server-fts** installato, è possibile aggiornare alla versione più recente con i comandi seguenti:

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

Se è necessaria un'installazione offline, individuare il download del pacchetto nella ricerca Full-text di [note sulla versione](sql-server-linux-release-notes.md). Usare quindi la stessa procedura di installazione offline descritta nell'articolo [Installare SQL Server](sql-server-linux-setup.md#offline).

## <a name="supported-languages"></a>Lingue supportate

Ricerca full-Text utilizza [word breaker](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) che determinano come identificare le singole parole basate sul linguaggio. È possibile ottenere un elenco di word breaker registrati eseguendo una query di **Sys. fulltext_languages** vista del catalogo. Con SQL Server vengono installati i Word breaker per le lingue seguenti:

| Linguaggio | ID della lingua |
|---|---|
| Lingua neutra | 0 |
| Arabo | 1025 |
| Bengali (India) | 1093 |
| Bokmål | 1044 |
| Portoghese (Brasile) | 1046 |
| Inglese (Regno Unito) | 2057 |
| Bulgaro | 1026 |
| Catalano | 1027 |
| Cinese (RAS di Hong Kong, Repubblica popolare cinese) | 3076 |
| Cinese (RAS di Macao) | 5124 |
| Cinese (Singapore) | 4100 |
| Croato | 1050 |
| Ceco | 1029 |
| Danese | 1030 |
| Olandese | 1043 |
| Inglese | 1033 |
| Francese | 1036 |
| Tedesco | 1031 |
| Greco | 1032 |
| Gujarati | 1095 |
| Ebraico | 1037 |
| Hindi | 1081 |
| Islandese | 1039 |
| Indonesiano | 1057 |
| Italiano | 1040 |
| Giapponese | 1041 |
| Kannada | 1099 |
| Coreano | 1042 |
| Lettone | 1062 |
| Lituano | 1063 |
| Malese (Malesia) | 1086 |
| Malayalam | 1100 |
| Marathi | 1102 |
| Polacco | 1045 |
| Portoghese | 2070 |
| Punjabi | 1094 |
| Rumeno | 1048 |
| Russo | 1049 |
| Serbo (alfabeto cirillico) | 3098 |
| Serbo (alfabeto latino) | 2074 |
| Cinese semplificato | 2052 |
| Slovacco | 1051 |
| Sloveno | 1060 |
| Spagnolo | 3082 |
| Svedese | 1053 |
| Tamil | 1097 |
| Telugu | 1098 |
| Thai | 1054 |
| Cinese tradizionale | 1028 |
| Turco | 1055 |
| Ucraino | 1058 |
| Urdu | 1056 |
| Vietnamita | 1066 |

## <a id="filters"></a> Filtri

Ricerca full-Text funziona anche con il testo archiviato in file binari. Ma in questo caso, è necessario un filtro installato per elaborare il file. Per altre informazioni sui filtri, vedere [configurare e gestire filtri per la ricerca](../relational-databases/search/configure-and-manage-filters-for-search.md).

È possibile visualizzare un elenco di filtri installati chiamando **sp_help_fulltext_system_components 'filter'** . Per SQL Server, vengono installati i filtri seguenti:

| Nome componente | ID classe | Version |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ANS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ASC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. asm | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.asp | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|ASX | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CLS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.csa | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.css | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|DOS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|DSP | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione DSW | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.HHC | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. HTML | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|HTX | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ICS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|IDL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.idq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|INF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|INX | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.mak | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Con estensione odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ODL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|PL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.PRC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|RCT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RGS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.SOL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|TAB | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TDL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.UDT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|URL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|con estensione vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|estensione vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>Ricerca semantica
[Ricerca semantica](../relational-databases/search/semantic-search-sql-server.md) si basa sulla funzionalità di ricerca Full-Text per estrarre e indicizzare statisticamente pertinenti *frasi chiave*. In questo modo è possibile eseguire una query il significato all'interno dei documenti nel database. È anche utile per identificare documenti simili.

Per usare la ricerca semantica, è necessario innanzitutto ripristinare il database Semantic Language Statistics nel computer.

1. Usare uno strumento, ad esempio [sqlcmd](sql-server-linux-setup-tools.md), per eseguire il comando Transact-SQL seguente nell'istanza di Linux di SQL Server. Questo comando Ripristina il database di statistiche lingua.

   ```sql
   RESTORE DATABASE [semanticsdb] FROM
   DISK = N'/opt/mssql/misc/semanticsdb.bak' WITH FILE = 1,
   MOVE N'semanticsdb' TO N'/var/opt/mssql/data/semanticsDB.mdf',
   MOVE N'semanticsdb_log' TO N'/var/opt/mssql/data/semanticsdb_log.ldf', NOUNLOAD, STATS = 5
   GO
   ```

   > [!NOTE]
   > Se necessario, aggiornare i percorsi nel comando RESTORE precedente in modo che la configurazione.

1. Eseguire il comando Transact-SQL seguente per registrare il database di statistiche lingua semantica.

    ```sql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO
    ```

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla ricerca Full-Text, vedere [ricerca Full-Text di SQL Server](../relational-databases/search/full-text-search.md). 
