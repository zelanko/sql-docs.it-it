---
title: Suggerimenti per l'uso di pacchetti R installati nelle librerie utente - servizi di SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee5dc9dc8b1730f26bada915d739f164a884801d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510778"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Suggerimenti per l'uso di pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo contiene sezioni separate per gli amministratori di database che non hanno familiarità con R e sviluppatori esperti di R che hanno l'accesso ai pacchetti familiarità in un'istanza di SQL Server.

## <a name="new-to-r"></a>Familiarità con R

Come amministratore di installazione di R per iniziare i pacchetti per la prima volta, conoscere che alcune nozioni di base sulla gestione dei pacchetti R possono aiutarti.

### <a name="package-dependencies"></a>Dipendenze dei pacchetti

I pacchetti R spesso dipendono da più altri pacchetti, alcuni dei quali potrebbero non essere disponibili nella libreria R predefinita utilizzata dall'istanza. A volte un pacchetto richiede una versione diversa di un pacchetto dipendente che è già installato. Le dipendenze dei pacchetti sono indicate in un file di descrizione incorporato nel pacchetto, ma in alcuni casi sono incomplete. È possibile usare un pacchetto chiamato [iGraph](https://igraph.org/r/) per articolare completamente il grafico delle dipendenze.

Se è necessario installare più pacchetti o si desidera assicurarsi che tutti gli utenti nell'organizzazione Ottiene il tipo di pacchetto corretto e la versione, è consigliabile usare la [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacchetto per analizzare la catena di dipendenza completa. minicRAN crea un repository locale che può essere condivisi tra più utenti o computer. Per altre informazioni, vedere [creare un repository di pacchetti locale usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>I formati, versioni e origini dei pacchetti

Sono presenti più origini per i pacchetti R, ad esempio [CRAN](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). Il sito ufficiale per il linguaggio R (<https://www.r-project.org/>) elenca molte di queste risorse. Microsoft mette a disposizione [MRAN](https://mran.microsoft.com/) per la distribuzione di R open source ([MRO](https://mran.microsoft.com/open)) e altri pacchetti. Molti pacchetti vengono pubblicati in GitHub, in cui gli sviluppatori possono ottenere il codice sorgente.

I pacchetti R eseguiti su più piattaforme di elaborazione. Assicurarsi che le versioni installate sono file binari di Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>La libreria che si sta installando a conoscere e i pacchetti che sono già installati.

Se è stato modificato in precedenza nell'ambiente R nel computer, prima di installare nulla, verificare che la variabile di ambiente R `.libPath` usi solo un percorso.

Questo percorso deve puntare alla cartella R_SERVICES per l'istanza. Per altre informazioni, incluse le procedure determinare quali pacchetti sono già installati, vedere [pacchetti predefinita di R e Python in SQL Server](installing-and-managing-r-packages.md).

## <a name="new-to-sql-server"></a>Novità di SQL Server

Gli sviluppatori R lavorare sul codice in esecuzione su SQL Server, i criteri di sicurezza protegge i server vincolano la possibilità di controllare l'ambiente R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Nelle librerie utente di R: non è supportata in SQL Server

Gli sviluppatori di R che desiderano installare nuovi pacchetti R sono abituati a installazione di pacchetti in base alle esigenze, utilizzando una privata e una libreria utente ogni volta che la libreria predefinita non è disponibile, oppure quando lo sviluppatore non è un amministratore nel computer. Ad esempio, in un ambiente di sviluppo R tipico, l'utente potrebbe aggiungere il percorso del pacchetto alla variabile di ambiente R `libPath`, o fare riferimento al percorso completo del pacchetto, simile al seguente:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Ciò non funziona durante l'esecuzione di soluzioni R in SQL Server, perché i pacchetti R devono essere installati in una raccolta predefinite specifiche che è associata l'istanza. Quando un pacchetto non è disponibile nella libreria predefinita, viene visualizzato questo errore quando si prova a chiamare il pacchetto:

*Errore nella libreria (xxx): nessun pacchetto denominato 'package-name'*

### <a name="avoid-package-not-found-errors"></a>Evitare gli errori "non trovato nel pacchetto"

+ Eliminare le dipendenze da librerie utente. 

    È una procedura di sviluppo non valido per installare pacchetti R necessari in una libreria utente personalizzato, perché può causare errori se una soluzione viene eseguita da un altro utente che non ha accesso al percorso della libreria.

    Inoltre, se un pacchetto viene installato nella libreria predefinita, il runtime R carica il pacchetto dalla libreria predefinita, anche se si specifica una versione diversa nel codice R.

+ Modificare il codice per l'esecuzione in un ambiente condiviso.

+ Evitare di installare i pacchetti come parte di una soluzione. Se si è autorizzati a installare i pacchetti, il codice avrà esito negativo. Anche se si è autorizzati a installare i pacchetti, è necessario effettuare quindi separatamente da altro codice che si desidera eseguire.

+ Controllare il codice per assicurarsi che non ci siano chiamate a pacchetti non installati.

+ Aggiornare il codice per rimuovere riferimenti diretti ai percorsi di librerie di R o i pacchetti R. 

+ Conoscere quale libreria di pacchetti è associata l'istanza. Per altre informazioni, vedere [pacchetti predefinita di R e Python in SQL Server](installing-and-managing-r-packages.md).

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)