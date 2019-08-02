---
title: Installare nuovi pacchetti di linguaggio R
description: Aggiungere nuovi pacchetti R a SQL Server 2016 R Services o SQL Server Machine Learning Services (in-database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1048dc6ef0a43c5fa41dd5398a5b3dced4a5ebe8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715099"
---
# <a name="install-new-r-packages-on-sql-server"></a>Installare nuovi pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come installare nuovi pacchetti R in un'istanza di SQL Server in cui è abilitato Machine Learning. Sono disponibili diversi metodi per l'installazione di nuovi pacchetti R, a seconda della versione di SQL Server disponibile e del fatto che il server disponga di una connessione Internet. Sono possibili gli approcci seguenti per l'installazione di nuovi pacchetti.

| Approccio                           | Permissions               | Remoto/locale |
|------------------------------------|---------------------------|--------------|
| [Usare i tradizionali gestori di pacchetti R](use-r-package-managers-on-sql-server.md)  | Admin | Local |
| [Usare RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Ruoli del database abilitati per l'amministratore in seguito | both|
| [Usare T-SQL (CREATE EXTERNAL LIBRARY)](install-r-packages-tsql.md) | Ruoli del database abilitati per l'amministratore in seguito | both 

## <a name="who-installs-permissions"></a>Utenti che installano (autorizzazioni)

La libreria di pacchetti R si trova fisicamente nella cartella programmi dell'istanza di SQL Server, in una cartella protetta con accesso limitato. Per scrivere in questo percorso sono necessarie le autorizzazioni di amministratore.

Gli non amministratori possono installare i pacchetti, ma in questo modo sono necessarie configurazioni e funzionalità aggiuntive non disponibili nelle installazioni iniziali. Esistono due approcci per le installazioni di pacchetti non amministrativi: RevoScaleR usando la versione 9.0.1 e versioni successive oppure usando CREATE EXTERNAL LIBRARY (solo SQL Server 2017). In SQL Server 2017, **dbo_owner** o un altro utente con l'autorizzazione Create external Library può installare pacchetti R nel database corrente.

Gli sviluppatori R sono abituati a creare librerie utente per i pacchetti necessari se le librerie situate in modo centralizzato sono fuori limite. Questa procedura è problematica per il codice R eseguito in un'istanza del motore di database SQL Server. SQL Server non è in grado di caricare pacchetti da librerie esterne, anche se tale libreria si trova nello stesso computer. Solo i pacchetti dalla libreria di istanze possono essere usati nel codice R eseguito in SQL Server.

L'accesso al file System viene in genere limitato nel server e anche se si dispone di diritti di amministratore e di accesso a una cartella del documento utente sul server, il runtime di script esterno eseguito in SQL Server non è in grado di accedere ai pacchetti installati al di fuori dell'istanza predefinita libreria. 

## <a name="considerations-for-package-installation"></a>Considerazioni sull'installazione dei pacchetti

Prima di installare nuovi pacchetti, valutare se le funzionalità abilitate da un determinato pacchetto sono adatte in un ambiente SQL Server. In un ambiente di SQL Server con protezione avanzata, è consigliabile evitare quanto segue:

+ Pacchetti per i quali è richiesto l'accesso alla rete
+ Pacchetti per i quali è richiesto l'accesso file system elevato
+ Il pacchetto viene usato per lo sviluppo Web o altre attività che non traggono vantaggio dall'esecuzione all'interno SQL Server

## <a name="offline-installation-no-internet-access"></a>Installazione offline (nessun accesso a Internet)

In generale, i server che ospitano i database di produzione bloccano le connessioni Internet. Per installare nuovi pacchetti R o Python in tali ambienti, è necessario preparare i pacchetti e le dipendenze in anticipo, quindi copiare i file in una cartella nel server per l'installazione offline.

L'identificazione di tutte le dipendenze diventa complicata. Per R, è consigliabile usare [miniCRAN per creare un repository locale](create-a-local-package-repository-using-minicran.md) e quindi trasferire il repository completamente definito in un'istanza di SQL Server isolata.

In alternativa, è possibile eseguire questi passaggi manualmente:

1. Identificare tutte le dipendenze del pacchetto. 
2. Controllare se nel server sono già installati i pacchetti necessari. Se il pacchetto è installato, verificare che la versione sia corretta.
3. Scaricare il pacchetto e tutte le dipendenze in un computer separato.
4. Spostare i file in una cartella accessibile dal server.
5. Eseguire un comando di installazione o un'istruzione DDL supportata per installare il pacchetto nella libreria di istanze di.

### <a name="download-the-package-as-a-zipped-file"></a>Scaricare il pacchetto come file compresso

Per l'installazione in un server senza accesso a Internet, è necessario scaricare una copia del pacchetto nel formato di un file compresso per l'installazione offline. **Non decomprimere il pacchetto.**

Ad esempio, la procedura seguente descrive ora come ottenere la versione corretta del pacchetto [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) da Bioconductor, supponendo che il computer abbia accesso a Internet.

1.  Nell'elenco **Archivi dei pacchetti** , individuare la versione **binaria di Windows** .

2.  Fare clic con il pulsante destro del mouse sul collegamento a. File ZIP e selezionare **Salva destinazione con nome**.

3.  Passare alla cartella locale in cui sono archiviati i pacchetti compressi, quindi fare clic su **Salva**.

    Questo processo crea una copia locale del pacchetto. 

4. Se si riceve un errore di download, provare con un altro sito mirror.

5. Dopo aver scaricato l'archivio pacchetti, è possibile installare il pacchetto o copiare il pacchetto compresso in un server che non dispone di accesso a Internet.

> [!TIP]
> Se per errore si installa il pacchetto invece di scaricare i file binari, nel computer verrà salvata anche una copia del file compresso scaricato. Controllare i messaggi di stato durante l'installazione del pacchetto per determinare il percorso del file. È possibile copiare il file compresso nel server che non dispone di accesso a Internet.
> 
> Tuttavia, quando si ottengono pacchetti utilizzando questo metodo, le dipendenze non vengono incluse. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Installazione side-by-side con server R o Python autonomi

Le funzionalità di R e Python sono incluse in diversi prodotti Microsoft, che possono coesistere nello stesso computer.

Se è stato installato SQL Server 2017 Microsoft Machine Learning Server (autonomo) o SQL Server 2016 R Server (standalone) oltre a analisi nel database (SQL Server Machine Learning Services e SQL Server 2016 R Services), il computer è separato installazioni di R per ogni, con duplicati di tutti gli strumenti e le librerie di R.

I pacchetti installati nella libreria R_SERVER vengono utilizzati solo da un server autonomo e non è possibile accedervi da un'istanza SQL Server (in-database). Utilizzare sempre la `R_SERVICES` libreria quando si installano i pacchetti che si desidera utilizzare nel database di in SQL Server. Per ulteriori informazioni sui percorsi, vedere [Package Library Location](../package-management/default-packages.md).

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)
