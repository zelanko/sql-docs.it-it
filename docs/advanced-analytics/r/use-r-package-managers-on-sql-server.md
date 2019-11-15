---
title: Usare i gestori di pacchetti R
description: Usare i comandi R standard come install.packages per aggiungere nuovi pacchetti R a R Services per SQL Server 2016 o Machine Learning Services per SQL Server (In-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633611"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usare strumenti di gestione pacchetti R per installare pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È possibile usare strumenti R standard per installare nuovi pacchetti in un'istanza di SQL Server 2016 o SQL Server 2017, a condizione che il computer abbia una porta 80 aperta e che si disponga dei diritti di amministratore.

> [!IMPORTANT] 
> Assicurarsi di installare i pacchetti nella libreria predefinita associata all'istanza corrente. Non installare mai i pacchetti in una directory utente.

Questa procedura usa RGui, ma è possibile usare RTerm o qualsiasi altro strumento da riga di comando R che supporta l'accesso con privilegi elevati.

## <a name="install-a-package-using-rgui"></a>Installare un pacchetto usando RGui

1. [Determinare il percorso della libreria di istanze](../package-management/r-package-information.md). Passare alla cartella in cui sono stati installati gli strumenti R. Il percorso predefinito per un'istanza predefinita di SQL Server 2017, ad esempio, è il seguente: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Fare clic con il pulsante destro del mouse su RGui.exe e scegliere **Esegui come amministratore**. Se non si hanno le autorizzazioni necessarie, contattare l'amministratore del database e fornire un elenco dei pacchetti necessari.

1. Dalla riga di comando, se si conosce il nome del pacchetto, è possibile digitare: `install.packages("the_package-name")` Le virgolette doppie sono obbligatorie per il nome del pacchetto.

1. Quando viene richiesto un sito mirror, selezionare qualsiasi sito comodo in base alla posizione.

Se il pacchetto di destinazione dipende da pacchetti aggiuntivi, il programma di installazione di R scarica automaticamente le dipendenze e le installa.

Se si hanno più istanze di SQL Server, ad esempio istanze affiancate di R Services per SQL Server 2016 e Machine Learning Services per SQL Server, eseguire l'installazione separatamente per ogni istanza se si vuole usare il pacchetto in entrambi i contesti. I pacchetti non possono essere condivisi tra istanze.

## <a name = "bkmk_offlineInstall"></a> Installazione offline tramite gli strumenti R

Se il server non ha accesso a Internet, per preparare i pacchetti sono necessari passaggi aggiuntivi. Per installare i pacchetti R in un server che non ha accesso a Internet, è necessario:

+ Analizzare le dipendenze in anticipo.
+ Scaricare il pacchetto di destinazione in un computer con accesso a Internet.
+ Scaricare tutti i pacchetti necessari nello stesso computer e inserire tutti i pacchetti in un unico archivio di pacchetti.
+ Comprimere l'archivio, se non è già in formato compresso.
+ Copiare l'archivio di pacchetti in un percorso nel server.
+ Installare il pacchetto di destinazione specificando il file di archivio come origine.

> [!IMPORTANT] 
>  Assicurarsi di analizzare tutte le dipendenze e scaricare **tutti** i pacchetti necessari **prima** di iniziare l'installazione. Per questo processo, è consigliabile usare [miniCRAN](https://mran.microsoft.com/package/miniCRAN). Questo pacchetto R accetta un elenco di pacchetti da installare, analizza le dipendenze e ottiene tutti i file compressi. miniCRAN crea quindi un singolo repository che è possibile copiare nel computer server. Per informazioni dettagliate, vedere [Creare un repository di pacchetti locale usando miniCRAN](create-a-local-package-repository-using-minicran.md)

Questa procedura presuppone che tutti i pacchetti necessari siano stati preparati, in formato compresso, e che siano pronti per la copia nel server.

1. Copiare il file compresso del pacchetto oppure, per più pacchetti, il repository completo contenente tutti i pacchetti in formato compresso, in un percorso a cui il server può accedere.

2. Aprire la cartella nel server in cui sono installati gli strumenti R per l'istanza. Se ad esempio si usa il prompt dei comandi di Windows in un sistema con R Services per SQL Server 2016, passare a `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Fare clic con il pulsante destro del mouse su RGui o RTerm e scegliere **Esegui come amministratore**.

4. Eseguire il comando R `install.packages` e specificare il nome del pacchetto o del repository e il percorso dei file compressi.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Questo comando consente di estrarre il pacchetto R `mynewpackage` dal file compresso locale, presupponendo che la copia sia stata salvata nella directory `C:\Temp\Downloaded packages`, quindi installa il pacchetto nel computer locale. Se il pacchetto ha dipendenze, il programma di installazione verifica la presenza di pacchetti esistenti nella libreria. Se è stato creato un repository che include le dipendenze, il programma di installazione installa anche i pacchetti necessari.

    Se i pacchetti necessari non sono presenti nella libreria di istanze e non è possibile trovarli nei file compressi, l'installazione del pacchetto di destinazione ha esito negativo.

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)
