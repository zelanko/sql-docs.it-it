---
title: Installare nuovi pacchetti di linguaggio R - servizi di SQL Server Machine Learning
description: Aggiungere nuovi pacchetti R per SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 590dbcc08d433147b61678c2b865ba205a0e547d
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432796"
---
# <a name="install-new-r-packages-on-sql-server"></a>Installare nuovi pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come installare nuovi pacchetti R in un'istanza di SQL Server in cui è abilitata l'apprendimento automatico. Esistono diversi metodi per installare nuovi pacchetti di R, a seconda di quale versione di SQL Server in uso e se il server dispone di una connessione a internet. Gli approcci seguenti per la nuova installazione del pacchetto sono possibili.

| Approccio                           | Permissions               | Remoto o locale |
|------------------------------------|---------------------------|--------------|
| [Usare i gestori di pacchetti R convenzionali](use-r-package-managers-on-sql-server.md)  | Amministrativi | Local |
| [Usare RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  Amministratore-abilitato, i ruoli del database in un secondo momento | both|
| [Usare T-SQL (CREATE EXTERNAL LIBRARY)](install-r-packages-tsql.md) | Amministratore-abilitato, i ruoli del database in un secondo momento | both 

## <a name="who-installs-permissions"></a>Che consente di installare (autorizzazioni)

La libreria di pacchetti R si trova fisicamente nella cartella file di programma dell'istanza di SQL Server, in una cartella sicura con accesso limitato. La scrittura in questa posizione richiede le autorizzazioni di amministratore.

I non amministratori possono installare i pacchetti, ma questa operazione richiede funzionalità non disponibili nelle installazioni iniziale e configurazione supplementari. Esistono due approcci per le installazioni del pacchetto senza privilegi di amministratore: RevoScaleR con versione 9.0.1 e versioni successive, o a utilizzare CREATE EXTERNAL LIBRARY (solo SQL Server 2017). In SQL Server 2017 **dbo_owner** o un altro utente con l'autorizzazione CREATE EXTERNAL LIBRARY è possibile installare pacchetti R nel database corrente.

Gli sviluppatori di R sono abituati alla creazione di librerie utente per i pacchetti di che cui hanno bisogno se ubicate centralmente le librerie sono inaccessibile. Questa pratica è problematica per il codice R eseguito in un'istanza di motore di database di SQL Server. SQL Server non è possibile caricare i pacchetti da librerie esterne, anche se tale libreria nello stesso computer. Nel codice R in esecuzione in SQL Server, è possono utilizzare solo i pacchetti della libreria di istanza.

Accesso al file system è in genere limitato sul server e anche se si dispone di diritti di amministratore e l'accesso a una cartella documenti utente sul server, il runtime dello script esterno che esegue SQL Server non è possibile accedere a tutti i pacchetti installati all'esterno dell'istanza predefinita libreria. 

## <a name="considerations-for-package-installation"></a>Considerazioni per l'installazione del pacchetto

Prima di installare nuovi pacchetti, considerare se la funzionalità abilitata per un determinato pacchetto sono appropriata in un ambiente di SQL Server. In un ambiente con protezione avanzato di SQL Server, si potrebbe voler evitare quanto segue:

+ Pacchetti che richiedono l'accesso alla rete
+ Pacchetti che richiedono Java o altri Framework non viene in genere usato in un ambiente di SQL Server
+ Pacchetti che richiedono l'accesso con privilegi elevati di file system
+ Pacchetto viene usato per lo sviluppo web o altre attività che non traggono vantaggio dall'esecuzione all'interno di SQL Server

## <a name="offline-installation-no-internet-access"></a>Installazione offline (Nessun accesso a internet)

In generale, i server che ospitano i database di produzione bloccano le connessioni internet. Installazione dei nuovi pacchetti R o Python in tali ambienti è necessario preparare in anticipo i pacchetti e le dipendenze e copiare i file in una cartella nel server per l'installazione offline.

Che identifica tutte le dipendenze diventa complicato. Per R, è consigliabile usare [miniCRAN per creare un repository locale](create-a-local-package-repository-using-minicran.md) e quindi trasferire il repository completamente definito in un'istanza di SQL Server isolata.

In alternativa, è possibile eseguire manualmente questa procedura:

1. Identificare tutte le dipendenze di pacchetto. 
2. Controllare se tutti i pacchetti necessari sono già installati nel server. Se il pacchetto viene installato, verificare che la versione sia corretta.
3. Scaricare il pacchetto e tutte le dipendenze in un computer separato.
4. Spostare i file in una cartella accessibile dal server.
5. Eseguire un comando di installazione supportati o l'istruzione DDL per installare il pacchetto nella libreria di istanza.

### <a name="download-the-package-as-a-zipped-file"></a>Scaricare il pacchetto come file compresso

Per l'installazione in un server senza accesso a internet, è necessario scaricare una copia del pacchetto nel formato di un file compresso per l'installazione offline. **Non decomprimere il pacchetto.**

Ad esempio, la procedura seguente descrive subito per ottenere la versione corretta del [FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacchetto da Bioconductor, presupponendo che il computer abbia accesso a internet.

1.  Nell'elenco **Archivi dei pacchetti** , individuare la versione **binaria di Windows** .

2.  Fare doppio clic sul collegamento per il. File con estensione ZIP e selezionare **Salva come**.

3.  Passare alla cartella locale in cui vengono archiviati i pacchetti compressi e fare clic su **salvare**.

    Questo processo crea una copia locale del pacchetto. 

4. Se si verifica un errore di download, provare a un sito mirror diversi.

5. Dopo aver scaricato l'archivio pacchetti, è possibile installare il pacchetto o copiare il pacchetto compresso in un server che non dispone dell'accesso a internet.

> [!TIP]
> Se per errore, si installa il pacchetto invece di scaricare i file binari, una copia del file compresso scaricato viene salvata anche nel computer. Controllare i messaggi di stato mentre l'installazione del pacchetto per determinare il percorso del file. È possibile copiare i file compressi nel server che non dispone dell'accesso a internet.
> 
> Tuttavia, quando si ottiene i pacchetti usando questo metodo, le dipendenze non vengono incluse. 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>Installazione side-by-side con Standalone R o Python server

Funzionalità di R e Python sono incluse in numerosi prodotti Microsoft, ognuno dei quali può coesistere nello stesso computer.

Se è installato SQL Server 2017 Microsoft Machine Learning Server (Standalone) o SQL Server 2016 R Server (Standalone) oltre a analitica nel database (SQL Server 2017 Machine Learning Services e SQL Server 2016 R Services), il computer dispone separato installazioni di R per ogni, con i duplicati di tutte le librerie e strumenti R.

I pacchetti installati nella libreria R_SERVER vengono usati solo da un server autonomo e non è possibile accedervi da un'istanza di SQL Server (In-Database). Usare sempre la `R_SERVICES` libreria quando si installano pacchetti che si desidera utilizzare nel database in SQL Server. Per altre informazioni sui percorsi, vedere [percorso di libreria del pacchetto](installing-and-managing-r-packages.md#package-library-location).


## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)