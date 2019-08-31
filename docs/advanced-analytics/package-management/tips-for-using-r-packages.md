---
title: Suggerimenti per l'uso di pacchetti R
description: Suggerimenti utili sull'uso di pacchetti R in SQL Server per coloro che non hanno familiarità con R o per SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/06/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5e283ab478a6d65243e9962fd5c26f5f91d87c15
ms.sourcegitcommit: 00350f6ffb73c2c0d99beeded61c5b9baa63d171
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70196344"
---
# <a name="tips-for-using-r-packages"></a>Suggerimenti per l'uso di pacchetti R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo fornisce suggerimenti utili sull'uso dei pacchetti R in SQL Server. Si tratta di suggerimenti per DBA che non hanno familiarità con R e sviluppatori R esperti che non hanno familiarità con l'accesso ai pacchetti in un'istanza di SQL Server.

## <a name="if-youre-new-to-r"></a>Se non si ha familiarità con R

Gli amministratori che installano i pacchetti R per la prima volta, conoscendo alcune nozioni di base sulla gestione dei pacchetti R possono essere utili per iniziare.

### <a name="package-dependencies"></a>Dipendenze del pacchetto

I pacchetti r spesso dipendono da più pacchetti, alcuni dei quali potrebbero non essere disponibili nella libreria R predefinita utilizzata dall'istanza di. A volte un pacchetto richiede una versione diversa di un pacchetto dipendente rispetto a quello già installato. Le dipendenze del pacchetto sono indicate in un file di descrizione incorporato nel pacchetto, ma talvolta incomplete. È possibile utilizzare un pacchetto denominato [iGraph](https://igraph.org/r/) per esprimere completamente il grafico delle dipendenze.

Se è necessario installare più pacchetti o si vuole garantire che tutti gli utenti dell'organizzazione ottengano il tipo di pacchetto e la versione corretti, si consiglia di usare il pacchetto [miniCRAN](https://mran.microsoft.com/package/miniCRAN) per analizzare la catena di dipendenze completa. minicRAN crea un repository locale che può essere condiviso tra più utenti o computer. Per altre informazioni, vedere [creare un repository di pacchetti locale usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Origini, versioni e formati del pacchetto

Sono disponibili più origini per i pacchetti R, ad esempio [Cran](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). Il sito ufficiale per il linguaggio R (<https://www.r-project.org/>) elenca molte di queste risorse. Microsoft offre [MRAN](https://mran.microsoft.com/) per la distribuzione di R ([riparazione](https://mran.microsoft.com/open)) open source e altri pacchetti. Molti pacchetti vengono pubblicati in GitHub, in cui gli sviluppatori possono ottenere il codice sorgente.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
I pacchetti R vengono eseguiti su più piattaforme di elaborazione. Assicurarsi che le versioni installate siano file binari di Windows.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
I pacchetti R vengono eseguiti su più piattaforme di elaborazione. Assicurarsi che le versioni installate siano file binari Linux.
::: moniker-end

### <a name="know-which-library-youre-installing-to-and-which-packages-are-already-installed"></a>Individuare la libreria in cui si sta eseguendo l'installazione e i pacchetti già installati

Se in precedenza è stato modificato l'ambiente r nel computer, prima di installare qualsiasi elemento, assicurarsi che la `.libPath` variabile di ambiente r usi un solo percorso.

Questo percorso deve puntare alla cartella R_SERVICES per l'istanza. Per altre informazioni, ad esempio su come determinare i pacchetti già installati, vedere [ottenere informazioni sui pacchetti R](../package-management/r-package-information.md).

## <a name="if-youre-new-to-sql-server"></a>Se non si ha familiarità con SQL Server

Gli sviluppatori R che lavorano sul codice in esecuzione in SQL Server, i criteri di sicurezza che proteggono il server vincolano la possibilità di controllare l'ambiente R. I suggerimenti seguenti descrivono situazioni tipiche e forniscono suggerimenti per l'uso di questo ambiente.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Librerie utente R: non supportate in SQL Server

Gli sviluppatori r che devono installare nuovi pacchetti R sono abituati a installare i pacchetti in modo, usando una libreria utente privata ogni volta che la libreria predefinita non è disponibile o quando lo sviluppatore non è un amministratore del computer. Ad esempio, in un ambiente di sviluppo r tipico, l'utente aggiunge il percorso del pacchetto alla variabile `libPath`di ambiente r o fa riferimento al percorso completo del pacchetto, come indicato di seguito:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Questa operazione non funziona quando si eseguono soluzioni R in SQL Server, perché i pacchetti R devono essere installati in una libreria predefinita specifica associata all'istanza. Quando un pacchetto non è disponibile nella libreria predefinita, viene ricevuto questo errore quando si tenta di chiamare il pacchetto:

*Errore nella libreria (xxx): nessun pacchetto denominato ' Package-Name '*

Per informazioni su come installare i pacchetti R in SQL Server, vedere [Install New r packages on SQL Server Machine Learning Services o R Services per SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="how-to-avoid-package-not-found-errors"></a>Come evitare errori di "pacchetto non trovato"

L'utilizzo delle linee guida seguenti consente di evitare gli errori di "pacchetto non trovato".

+ Eliminare le dipendenze dalle librerie utente.

    Si tratta di una procedura di sviluppo non valida per installare i pacchetti R necessari in una libreria utente personalizzata. Questo può causare errori se una soluzione viene eseguita da un altro utente che non ha accesso al percorso della libreria.

    Inoltre, se un pacchetto è installato nella libreria predefinita, il runtime di R carica il pacchetto dalla libreria predefinita, anche se si specifica una versione diversa nel codice R.

+ Verificare che il codice sia in grado di essere eseguito in un ambiente condiviso.

+ Evitare di installare pacchetti come parte di una soluzione. Se non si dispone delle autorizzazioni per installare i pacchetti, il codice avrà esito negativo. Anche se si dispone delle autorizzazioni per installare i pacchetti, è necessario eseguire questa operazione separatamente rispetto a quello che si desidera eseguire.

+ Controllare il codice per assicurarsi che non ci siano chiamate a pacchetti non installati.

+ Aggiornare il codice per rimuovere i riferimenti diretti ai percorsi dei pacchetti R o delle librerie R.

+ Sa quale libreria di pacchetti è associata all'istanza di. Per altre informazioni, vedere [ottenere informazioni sul pacchetto R](../package-management/r-package-information.md).

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)