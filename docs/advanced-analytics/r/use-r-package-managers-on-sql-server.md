---
title: Usare i gestori di pacchetti R - servizi di SQL Server Machine Learning
description: Usare i comandi R standard, ad esempio Packages per aggiungere nuovi pacchetti R per SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database).
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6012fb1a3376c00a64239e0fbf10115b8a4367d8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510388"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>Utilizzare i gestori di pacchetti R per installare pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

È possibile usare gli strumenti R standard per installare nuovi pacchetti in un'istanza di SQL Server 2016 o SQL Server 2017, fornendo il computer ha una porta 80 aperta e si dispone di diritti di amministratore.

> [!IMPORTANT] 
> Assicurarsi di installare i pacchetti nella libreria predefinita associata all'istanza corrente. Non installare mai i pacchetti in una directory utente.

Questa procedura Usa RGui ma è possibile usare qualsiasi altro R della riga di comando strumento che supporta l'accesso con privilegi elevato o RTerm.

## <a name="install-a-package-using-rgui"></a>Installare un pacchetto utilizzando RGui

1. [Determinare il percorso della libreria di istanza](installing-and-managing-r-packages.md). Passare alla cartella in cui sono installati gli strumenti R. Ad esempio, il percorso predefinito per un'istanza predefinita di SQL Server 2017 è come segue: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. RGui.exe e scegliere **Esegui come amministratore**. Se non hai le autorizzazioni necessarie, contattare l'amministratore del database e fornire un elenco dei pacchetti che necessari.

1. Dalla riga di comando, se si conosce il nome del pacchetto, è possibile digitare: `install.packages("the_package-name")` Le virgolette doppie sono necessari per il nome del pacchetto.

1. Quando viene richiesto un sito mirror, selezionare tutti i siti che sono utile per il percorso.

Se il pacchetto di destinazione dipende da pacchetti aggiuntivi, il programma di installazione di R automaticamente le dipendenze vengono scaricate e li installa automaticamente.

Se si dispone di più istanze di SQL Server, ad esempio le istanze side-by-side di SQL Server 2016 R Services e SQL Server 2017 Machine Learning Services, eseguire l'installazione separatamente per ogni istanza se si desidera usare il pacchetto in entrambi i contesti. I pacchetti non possono essere condivisi tra più istanze.

## <a name = "bkmk_offlineInstall"></a> Installazione offline usando gli strumenti R

Se il server non ha accesso a internet, sono necessari passaggi aggiuntivi per preparare i pacchetti. Per installare pacchetti R in un server che non dispone dell'accesso a internet, è necessario:

+ Analizzare le dipendenze in anticipo.
+ Scaricare il pacchetto di destinazione in un computer con accesso a Internet.
+ Scaricare tutti i pacchetti necessari con lo stesso computer e inserire tutti i pacchetti in un archivio unico pacchetto.
+ L'archivio ZIP se non è già in formato compresso.
+ Copiare l'archivio di pacchetti in un percorso nel server.
+ Installare il pacchetto di destinazione specificare il file di archivio come origine.

> [!IMPORTANT] 
>  Assicurarsi che si analizza tutte le dipendenze e scaricare **tutte** i pacchetti necessari **prima di** iniziare l'installazione. È consigliabile [miniCRAN](https://mran.microsoft.com/package/miniCRAN) per questo processo. Questo pacchetto R accetta un elenco dei pacchetti da installare, analizza le dipendenze e ottiene tutti i file compressi automaticamente. miniCRAN crea quindi un singolo repository che è possibile copiare nel computer server. Per informazioni dettagliate, vedere [creare un repository di pacchetti locale usando miniCRAN](create-a-local-package-repository-using-minicran.md)

Questa procedura presuppone di aver preparato tutti i pacchetti che è necessario, in formato compresso e sono pronti per copiarli nel server.

1. Copia il pacchetto compressi in file o per più pacchetti, il repository completo che contiene tutti i pacchetti compressi in formato, in un percorso accessibile al server.

2. Aprire la cartella nel server in cui sono installati gli strumenti R per l'istanza. Ad esempio, se si usa il prompt dei comandi di Windows in un sistema con SQL Server 2016 R Services, passare a `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Fare clic su RGui o RTerm e selezionare **Esegui come amministratore**.

4. Eseguire il comando R `install.packages` e specificare il pacchetto o nome del repository e il percorso dei file compressi.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Questo comando estrae il pacchetto R `mynewpackage` dal file compresso locale, presupponendo che la copia è stato salvato nella directory `C:\Temp\Downloaded packages`e installa il pacchetto nel computer locale. Se il pacchetto include tutte le dipendenze, il programma di installazione cerca i pacchetti esistenti nella raccolta. Se è stato creato un repository che include le dipendenze, il programma di installazione installa anche i pacchetti necessari.

    Se tutti i pacchetti necessari non sono presenti nella libreria di istanza e non sono stati trovati nei file compressi, l'installazione del pacchetto di destinazione ha esito negativo.

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)
