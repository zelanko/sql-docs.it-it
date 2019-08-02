---
title: Suggerimenti per l'uso di pacchetti R installati nelle librerie utente
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16f3ae10c7a05529c86bea5684182c7805f9f54b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715677"
---
# <a name="tips-for-using-r-packages-in-sql-server"></a>Suggerimenti per l'uso di pacchetti R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo contiene sezioni separate per DBA che non hanno familiarità con R e sviluppatori R esperti che non hanno familiarità con l'accesso ai pacchetti in un'istanza di SQL Server.

## <a name="new-to-r"></a>Nuovo a R

Gli amministratori che installano i pacchetti R per la prima volta, conoscendo alcune nozioni di base sulla gestione dei pacchetti R possono essere utili per iniziare.

### <a name="package-dependencies"></a>Dipendenze del pacchetto

I pacchetti r spesso dipendono da più pacchetti, alcuni dei quali potrebbero non essere disponibili nella libreria R predefinita utilizzata dall'istanza di. A volte un pacchetto richiede una versione diversa di un pacchetto dipendente che è già installato. Le dipendenze del pacchetto sono indicate in un file di descrizione incorporato nel pacchetto, ma talvolta incomplete. È possibile utilizzare un pacchetto denominato [iGraph](https://igraph.org/r/) per esprimere completamente il grafico delle dipendenze.

Se è necessario installare più pacchetti o si vuole garantire che tutti gli utenti dell'organizzazione ottengano il tipo di pacchetto e la versione corretti, si consiglia di usare il pacchetto [miniCRAN](https://mran.microsoft.com/package/miniCRAN) per analizzare la catena di dipendenze completa. minicRAN crea un repository locale che può essere condiviso tra più utenti o computer. Per altre informazioni, vedere [creare un repository di pacchetti locale usando miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="package-sources-versions-and-formats"></a>Origini, versioni e formati del pacchetto

Sono disponibili più origini per i pacchetti R, ad esempio [Cran](https://cran.r-project.org/) e [Bioconductor](https://www.bioconductor.org/). Il sito ufficiale per il linguaggio R (<https://www.r-project.org/>) elenca molte di queste risorse. Microsoft offre [MRAN](https://mran.microsoft.com/) per la distribuzione di R ([riparazione](https://mran.microsoft.com/open)) open source e altri pacchetti. Molti pacchetti vengono pubblicati in GitHub, in cui gli sviluppatori possono ottenere il codice sorgente.

I pacchetti R vengono eseguiti su più piattaforme di elaborazione. Assicurarsi che le versioni installate siano file binari di Windows.

### <a name="know-which-library-you-are-installing-to-and-which-packages-are-already-installed"></a>Individuare la libreria in cui si esegue l'installazione e i pacchetti già installati.

Se in precedenza è stato modificato l'ambiente r nel computer, prima di installare qualsiasi elemento, assicurarsi che la variabile `.libPath` di ambiente r usi un solo percorso.

Questo percorso deve puntare alla cartella R_SERVICES per l'istanza. Per altre informazioni, ad esempio su come determinare i pacchetti già installati, vedere [pacchetti R e Python predefiniti in SQL Server](../package-management/default-packages.md).

## <a name="new-to-sql-server"></a>Nuovo SQL Server

Gli sviluppatori R che lavorano sul codice in esecuzione in SQL Server, i criteri di sicurezza che proteggono il server vincolano la possibilità di controllare l'ambiente R.

### <a name="r-user-libraries-not-supported-on-sql-server"></a>Librerie utente R: non supportate in SQL Server

Gli sviluppatori r che devono installare nuovi pacchetti R sono abituati a installare i pacchetti in modo, usando una libreria utente privata ogni volta che la libreria predefinita non è disponibile o quando lo sviluppatore non è un amministratore del computer. Ad esempio, in un ambiente di sviluppo r tipico, l'utente aggiunge il percorso del pacchetto alla variabile `libPath`di ambiente r o fa riferimento al percorso completo del pacchetto, come indicato di seguito:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Questa operazione non funziona quando si eseguono soluzioni R in SQL Server, perché i pacchetti R devono essere installati in una libreria predefinita specifica associata all'istanza. Quando un pacchetto non è disponibile nella libreria predefinita, viene ricevuto questo errore quando si tenta di chiamare il pacchetto:

*Errore nella libreria (xxx): nessun pacchetto denominato ' Package-Name '*

### <a name="avoid-package-not-found-errors"></a>Evitare gli errori di "pacchetto non trovato"

+ Eliminare le dipendenze dalle librerie utente. 

    Non è consigliabile installare i pacchetti R necessari in una libreria utente personalizzata, in quanto può causare errori se una soluzione viene eseguita da un altro utente che non ha accesso al percorso della libreria.

    Inoltre, se un pacchetto è installato nella libreria predefinita, il runtime di R carica il pacchetto dalla libreria predefinita, anche se si specifica una versione diversa nel codice R.

+ Modificare il codice per l'esecuzione in un ambiente condiviso.

+ Evitare di installare pacchetti come parte di una soluzione. Se non si dispone delle autorizzazioni per installare i pacchetti, il codice avrà esito negativo. Anche se si dispone delle autorizzazioni per installare i pacchetti, è necessario eseguire questa operazione separatamente rispetto a quello che si desidera eseguire.

+ Controllare il codice per assicurarsi che non ci siano chiamate a pacchetti non installati.

+ Aggiornare il codice per rimuovere i riferimenti diretti ai percorsi dei pacchetti R o delle librerie R. 

+ Sa quale libreria di pacchetti è associata all'istanza di. Per altre informazioni, vedere [pacchetti R e Python predefiniti in SQL Server](../package-management/default-packages.md).

## <a name="see-also"></a>Vedere anche

+ [Installare nuovi pacchetti R](install-additional-r-packages-on-sql-server.md)
+ [Installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Esercitazioni, esempi, soluzioni](../tutorials/machine-learning-services-tutorials.md)