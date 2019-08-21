---
title: Usare i gestori di pacchetti R
description: Usare i comandi R standard come install. Packages per aggiungere nuovi pacchetti R a SQL Server 2016 R Services o SQL Server Machine Learning Services (in-database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633611"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Usare i gestori di pacchetti R per installare i pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

È possibile usare gli strumenti R standard per installare nuovi pacchetti in un'istanza di SQL Server 2016 o SQL Server 2017, a condizione che il computer disponga di una porta 80 aperta e che si disponga dei diritti di amministratore.

> [!IMPORTANT] 
> Assicurarsi di installare i pacchetti nella libreria predefinita associata all'istanza corrente. Non installare mai i pacchetti in una directory utente.

Questa procedura usa RGui, ma è possibile usare RTerm o qualsiasi altro strumento da riga di comando R che supporta l'accesso con privilegi elevati.

## <a name="install-a-package-using-rgui"></a>Installare un pacchetto usando RGui

1. [Determinare il percorso della libreria di istanze](../package-management/r-package-information.md). Passare alla cartella in cui sono installati gli strumenti R. Il percorso predefinito per un'istanza predefinita di SQL Server 2017, ad esempio, è il seguente:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. Fare clic con il pulsante destro del mouse su RGui. exe e scegliere **Esegui come amministratore**. Se non si dispone delle autorizzazioni necessarie, contattare l'amministratore del database e fornire un elenco dei pacchetti necessari.

1. Dalla riga di comando, se si conosce il nome del pacchetto, è possibile digitare: `install.packages("the_package-name")`Per il nome del pacchetto sono necessarie virgolette doppie.

1. Quando viene richiesto un sito mirror, selezionare un sito appropriato per la propria posizione.

Se il pacchetto di destinazione dipende da pacchetti aggiuntivi, il programma di installazione di R scaricherà automaticamente le dipendenze e le installerà automaticamente.

Se si dispone di più istanze di SQL Server, ad esempio istanze affiancate di SQL Server 2016 R Services e SQL Server Machine Learning Services, eseguire l'installazione separatamente per ogni istanza se si desidera utilizzare il pacchetto in entrambi i contesti. I pacchetti non possono essere condivisi tra istanze.

## <a name = "bkmk_offlineInstall"></a>Installazione offline con strumenti R

Se il server non dispone di accesso a Internet, per preparare i pacchetti sono necessari passaggi aggiuntivi. Per installare i pacchetti R in un server che non dispone di accesso a Internet, è necessario:

+ Analizzare le dipendenze in anticipo.
+ Scaricare il pacchetto di destinazione in un computer con accesso a Internet.
+ Scaricare tutti i pacchetti necessari nello stesso computer e inserire tutti i pacchetti in un unico archivio pacchetti.
+ Se non è già in formato compresso, comprimere l'archivio.
+ Copiare l'archivio del pacchetto in un percorso nel server.
+ Installare il pacchetto di destinazione specificando il file di archivio come origine.

> [!IMPORTANT] 
>  Assicurarsi di analizzare tutte le dipendenze e scaricare **tutti i** pacchetti necessari **prima** di iniziare l'installazione. Per questo processo è consigliabile [miniCRAN](https://mran.microsoft.com/package/miniCRAN) . Questo pacchetto R accetta un elenco di pacchetti che si vuole installare, analizza le dipendenze e ottiene tutti i file compressi. miniCRAN crea quindi un singolo repository che è possibile copiare nel computer server. Per informazioni dettagliate, vedere [creare un repository di pacchetti locale con miniCRAN](create-a-local-package-repository-using-minicran.md)

In questa procedura si presuppone che siano stati preparati tutti i pacchetti necessari, in formato compresso, e che siano pronti per la copia nel server.

1. Copiare il file compresso del pacchetto o per più pacchetti, il repository completo che contiene tutti i pacchetti in formato compresso, in una posizione a cui il server può accedere.

2. Aprire la cartella nel server in cui sono installati gli strumenti R per l'istanza. Se ad esempio si usa il prompt dei comandi di Windows in un sistema con SQL Server 2016 R Services, passare a `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Fare clic con il pulsante destro del mouse su RGui o RTerm e scegliere **Esegui come amministratore**.

4. Eseguire il comando `install.packages` R e specificare il nome del pacchetto o del repository e il percorso dei file compressi.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Questo comando estrae il pacchetto `mynewpackage` R dal file compresso locale, presupponendo che la copia sia stata salvata nella directory `C:\Temp\Downloaded packages`e che il pacchetto venga installato nel computer locale. Se il pacchetto presenta dipendenze, il programma di installazione verifica la presenza di pacchetti esistenti nella libreria. Se è stato creato un repository che include le dipendenze, il programma di installazione installa anche i pacchetti necessari.

    Se nella libreria di istanze non è presente alcun pacchetto necessario e non è possibile trovarlo nei file compressi, l'installazione del pacchetto di destinazione ha esito negativo.

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)
