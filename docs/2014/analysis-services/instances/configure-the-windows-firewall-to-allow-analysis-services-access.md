---
title: Configurare la Windows Firewall per consentire l'accesso Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b74c767c50e8a62c2d65ad089e386a94b9c8a5e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151854"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>Configurare Windows Firewall per consentire l'accesso ad Analysis Services
  Un primo passaggio importante per rendere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] disponibile nella rete consiste nel determinare se è necessario sbloccare le porte in un firewall. Per la maggior parte delle installazioni è necessario creare almeno una regola del firewall in entrata per consentire le connessioni a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 I requisiti di configurazione del firewall variano in base alla modalità di installazione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   Aprire la porta TCP 2383 quando si installa un'istanza predefinita o si crea un cluster di failover di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Aprire la porta TCP 2382 quando si installa un'istanza denominata. Per le istanze denominate vengono utilizzate assegnazioni di porte dinamiche. Come servizio di individuazione per Analysis Services, il servizio SQL Server Browser rimane in ascolto sulla porta TCP 2382 e reindirizza la richiesta di connessione alla porta attualmente utilizzata da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Aprire la porta TCP 2382 quando si installa [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint per supportare [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. In [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è esterna a SharePoint. Le richieste in ingresso all'istanza denominata "PowerPivot" provengono da applicazioni Web di SharePoint su una connessione di rete e richiedono una porta aperta. Come per altre istanze denominate di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , creare una regola in ingresso per il servizio SQL Server Browser sulla porta TCP 2382 per consentire l'accesso a [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
-   Per [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 non aprire porte in Windows Firewall. Come componente aggiuntivo per SharePoint, il servizio utilizza porte configurate per SharePoint e stabilisce solo connessioni locali all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che carica ed esegue query sui modelli di dati di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le istanze in esecuzione in macchine virtuali di Azure, utilizzare istruzioni alternative per la configurazione dell'accesso al server. Vedere [SQL Server Business Intelligence in macchine virtuali di Azure](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx).  
  
 Anche se l'istanza predefinita [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di è in ascolto sulla porta TCP 2383, è possibile configurare il server in modo che sia in ascolto su una porta fissa diversa, connettendosi \<al server nel\<formato: nomeserver >: NumeroPorta >.  
  
 È possibile utilizzare una sola porta TCP per un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In computer che dispongono di più schede di rete o più indirizzi IP, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è in ascolto su una porta TCP per tutti gli indirizzi IP assegnati o con alias al computer. In caso di requisiti specifici per più porte, provare a configurare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'accesso HTTP. In questo modo è possibile configurare più endpoint HTTP su qualsiasi porta si desideri. Vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Controllare le impostazioni del firewall e delle porte per Analysis Services](#bkmk_checkport)  
  
-   [Configurare Windows Firewall per un'istanza predefinita di Analysis Services](#bkmk_default)  
  
-   [Configurare l'accesso a Windows Firewall per un'istanza denominata di Analysis Services](#bkmk_named)  
  
-   [Configurazione delle porte per un cluster di Analysis Services](#bkmk_cluster)  
  
-   [Configurazione porta per PowerPivot per SharePoint](#bkmk_powerpivot)  
  
-   [Utilizzare una porta fissa per un'istanza predefinita o denominata di Analysis Services](#bkmk_fixed)  
  
 Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="bkmk_checkport"></a> Controllare le impostazioni del firewall e delle porte per Analysis Services  
 Nei sistemi operativi Microsoft Windows supportati da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Windows Firewall è attivato per impostazione predefinita e blocca le connessioni remote. È necessario aprire manualmente una porta nel firewall per consentire le richieste in entrata per Analysis Services. Questo passaggio non viene eseguito dal programma di installazione di SQL Server.  
  
 Le impostazioni delle porte sono specificate nel file msmdsrv.ini e nella pagina delle Proprietà generali di un'istanza di Analysis Services in SQL Server Management Studio. Se il valore di `Port` è impostato su un numero intero positivo, il servizio è in ascolto su una porta fissa. Se il valore di `Port` è impostato su 0, il servizio è in ascolto sulla porta 2383 se si tratta dell'istanza predefinita o su una porta assegnata dinamicamente se si tratta di un'istanza denominata.  
  
 Le assegnazioni di porte dinamiche vengono utilizzate solo per le istanze denominate. Il servizio `MSOLAP$InstanceName` è in grado di determinare la porta da utilizzare all'avvio. Per determinare il numero effettivo della porta in uso da un'istanza denominata, effettuare le operazioni seguenti:  
  
-   Avviare Gestione attività e fare clic su **Servizi** per ottenere il PID del `MSOLAP$InstanceName`.  
  
-   Eseguire `netstat -ao -p TCP` dalla riga di comando per visualizzare le informazioni sulla porta TCP per tale PID.  
  
-   Verificare la porta utilizzando SQL Server Management Studio e connettersi a un server Analysis Services nel formato seguente: \<IPAddress >:\<NumeroPorta >.  
  
 Sebbene un'applicazione possa essere in ascolto su una porta specifica, le connessioni non riescono se l'accesso è bloccato da un firewall. Per consentire alle connessioni di raggiungere un'istanza denominata di Analysis Services, è necessario sbloccare nel firewall l'accesso a msmdsrv.exe o alla porta fissa su cui è in ascolto. Nelle restanti sezioni di questo argomento vengono fornite le istruzioni necessarie per questa operazione.  
  
 Per controllare se le impostazioni del firewall sono già definite per Analysis Services, utilizzare Windows Firewall con sicurezza avanzata nel Pannello di controllo. Nella pagina Firewall della cartella Monitoraggio è visualizzato un elenco completo delle regole definite per il server locale.  
  
 Si noti che per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]tutte le regole del firewall devono essere definite manualmente. Anche se in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e SQL Server Browser vengono riservate le porte 2382 e 2383, tramite il programma di installazione di SQL Server o gli strumenti di configurazione non è possibile definire regole del firewall per consentire l'accesso alle porte o ai file eseguibili dei programmi.  
  
##  <a name="bkmk_default"></a> Configurare Windows Firewall per un'istanza predefinita di Analysis Services  
 L'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è in ascolto sulla porta TCP 2383. Se è stata installata l'istanza predefinita e si desidera utilizzare questa porta, è sufficiente sbloccare l'accesso in ingresso alla porta TCP 2383 in Windows Firewall per abilitare l'accesso remoto per l'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se è stata installata l'istanza predefinita, ma si desidera configurare il servizio in modo che sia in attesa su una porta fissa, vedere [Utilizzare una porta fissa per un'istanza predefinita o denominata di Analysis Services](#bkmk_fixed) di seguito in questo argomento.  
  
 Per verificare se il servizio è in esecuzione come istanza predefinita (MSSQLServerOLAPService), controllare il relativo nome in Gestione configurazione SQL Server. Un'istanza predefinita di Analysis Services è sempre elencata come **SQL Server Analysis Services (MSSQLSERVER)** .  
  
> [!NOTE]  
>  Nei vari sistemi operativi Windows sono disponibili strumenti diversi per la configurazione di Windows Firewall. La maggior parte di questi strumenti consente di scegliere tra l'apertura di una porta specifica o di un eseguibile di un programma. A meno che non vi sia un motivo per specificare l'eseguibile di un programma, è consigliabile specificare la porta.  
  
 Quando si specifica una regola in ingresso, adottare una convenzione di denominazione che consenta di individuare in modo semplice le regole in un secondo momento, ad esempio **SQL Server Analysis Services (TCP-in) 2383**.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Windows Firewall con sicurezza avanzata  
  
1.  Nel Pannello di controllo di Windows 7 o Windows Vista fare clic su **Sistema e sicurezza**, selezionare **Windows Firewall**, quindi fare clic su **Impostazioni avanzate**. In Windows Server 2008 o 2008 R2 aprire Strumenti di amministrazione e fare clic su **Windows Firewall con protezione avanzata**. In Windows Server 2012 aprire la pagina Applicazioni e digitare **Windows Firewall**.  
  
2.  Fare clic con il pulsante destro del mouse su **Regole connessioni in entrata** e scegliere **Nuova regola**.  
  
3.  In tipo di regola fare `Port` clic su Avanti e quindi su **Avanti**.  
  
4.  In protocollo e porte selezionare **TCP** e quindi digitare `2383` **porte locali specifiche**.  
  
5.  In Azione fare clic su **Consenti la connessione** , quindi su **Avanti**.  
  
6.  In Profilo deselezionare tutti i percorsi di rete non applicabili, quindi fare clic su **Avanti**.  
  
7.  In nome digitare un nome descrittivo per questa regola (ad esempio, `SQL Server Analysis Services (tcp-in) 2383`) e quindi fare clic su **fine**.  
  
8.  Per verificare che le connessioni remote siano abilitate, aprire SQL Server Management Studio o Excel in un computer diverso e connettersi a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificando il nome di rete del server in **Nome server**.  
  
    > [!NOTE]  
    >  Gli altri utenti non potranno accedere a questo server fino a quando non riceveranno le autorizzazioni. Per altre informazioni, vedere [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md).  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintassi di netsh advfirewall  
  
-   Tramite il comando seguente è possibile creare una regola per le connessioni in ingresso che consente le richieste in ingresso sulla porta TCP 2383.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> Configurare l'accesso a Windows Firewall per un'istanza denominata di Analysis Services  
 Le istanze denominate di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] possono essere in ascolto su una porta fissa o su una porta assegnata dinamicamente, dove il servizio SQL Server Browser fornisce le informazioni di connessione valide per il servizio al momento della connessione.  
  
 Il servizio SQL Server Browser è in ascolto sulla porta TCP 2382. UDP non viene utilizzato. TCP è l'unico protocollo di trasmissione utilizzato da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Scegliere uno degli approcci seguenti per abilitare l'accesso remoto a un'istanza denominata di Analysis Services:  
  
-   Utilizzare assegnazioni di porta dinamiche e il servizio SQL Server Browser. Sbloccare la porta utilizzata dal servizio SQL Server Browser in Windows Firewall. Connettersi al server nel formato seguente: \<nomeserver >\\< NomeIstanza\>.  
  
-   Utilizzare insieme una porta fissa e il servizio SQL Server Browser. Questo approccio consente di connettersi utilizzando il formato \<nomeserver >\\< NomeIstanza\>, identico all'approccio di assegnazione porta dinamica, con la differenza che in questo caso il server è in ascolto su una porta fissa. In questo scenario, il servizio SQL Server Browser fornisce la risoluzione dei nomi all'istanza di Analysis Services che è in attesa sulla porta fissa. Per utilizzare questo approccio, configurare il server in modo che sia in attesa su una porta fissa, sbloccare l'accesso a tale porta e sbloccare l'accesso alla porta utilizzata dal servizio SQL Server Browser.  
  
 Il servizio SQL Server Browser viene utilizzato solo con istanze denominate, mai con l'istanza predefinita. Il servizio viene installato automaticamente ed è abilitato quando si installa una qualsiasi funzionalità di SQL Server come istanza denominata. Se si sceglie un approccio che richiede il servizio SQL Server Browser, accertarsi che rimanga abilitato e avviato nel server.  
  
 Se non è possibile utilizzare il servizio SQL Server Browser, è necessario assegnare una porta fissa nella stringa di connessione ignorando la risoluzione dei nomi di dominio. Senza il servizio SQL Server Browser, in tutte le connessioni client deve essere incluso il numero di porta nella stringa di connessione (ad esempio, AW-SRV01: 54321).  
  
 **Opzione 1: Usare le assegnazioni di porta dinamiche e sbloccare l'accesso al servizio SQL Server Browser**  
  
 Le assegnazioni di porta dinamiche per le istanze denominate di Analysis Services vengono stabilite da `MSOLAP$InstanceName` all'avvio del servizio. Per impostazione predefinita, il servizio richiede il primo numero di porta disponibile trovato, utilizzando un numero di porta diverso ogni volta che viene riavviato.  
  
 La risoluzione dei nomi di istanza viene gestita dal servizio SQL Server Browser. Se si utilizzano assegnazioni di porta dinamiche con un'istanza denominata, è sempre necessario sbloccare la porta TCP 2382 per il servizio SQL Server Browser.  
  
> [!NOTE]  
>  Il servizio SQL Server Browser è in ascolto su entrambe le porte UDP 1434 e TCP 2382, rispettivamente per il Motore di database e per Analysis Services. Anche se è già stata sbloccata la porta UDP 1434 per il servizio SQL Server Browser, è comunque necessario sbloccare anche la porta TCP 2382 per Analysis Services.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Windows Firewall con sicurezza avanzata  
  
1.  Nel Pannello di controllo di Windows 7 o Windows Vista fare clic su **Sistema e sicurezza**, selezionare **Windows Firewall**, quindi fare clic su **Impostazioni avanzate**. In Windows Server 2008 o 2008 R2 aprire Strumenti di amministrazione e fare clic su **Windows Firewall con protezione avanzata**. In Windows Server 2012 aprire la pagina Applicazioni e digitare **Windows Firewall**.  
  
2.  Per sbloccare l'accesso al servizio SQL Server Browser, fare clic con il pulsante destro del mouse su **Regole connessioni in entrata** , quindi scegliere **Nuova regola**.  
  
3.  In tipo di regola fare `Port` clic su Avanti e quindi su **Avanti**.  
  
4.  In protocollo e porte selezionare **TCP** e quindi digitare `2382` **porte locali specifiche**.  
  
5.  In Azione fare clic su **Consenti la connessione** , quindi su **Avanti**.  
  
6.  In Profilo deselezionare tutti i percorsi di rete non applicabili, quindi fare clic su **Avanti**.  
  
7.  In nome digitare un nome descrittivo per questa regola (ad esempio, `SQL Server Browser Service (tcp-in) 2382`) e quindi fare clic su **fine**.  
  
8.  Per verificare che le connessioni remote siano abilitate, aprire SQL Server Management Studio o Excel in un computer diverso e connettersi al Analysis Services specificando il nome di rete del server e il nome dell'istanza nel formato \<nomeserver > \\< NomeIstanza\>. Ad esempio, su un server denominato **AW-SRV01** con un'istanza denominata **Finance**, il nome server è **AW-SRV01\Finance**.  
  
 **Opzione 2: Utilizzare una porta fissa per un'istanza denominata**  
  
 In alternativa, è possibile assegnare una porta fissa e quindi sbloccare l'accesso a tale porta. Questo approccio offre capacità di controllo migliori rispetto a consentire l'accesso al file eseguibile di un programma. Per questo motivo, per accedere a una qualsiasi istanza di Analysis Services è consigliabile utilizzare una porta fissa.  
  
 Per assegnare una porta fissa, seguire le istruzioni in [Utilizzare una porta fissa per un'istanza predefinita o denominata di Analysis Services](#bkmk_fixed) in questo argomento, quindi tornare a questa sezione per sbloccare la porta.  
  
#### <a name="windows-firewall-with-advanced-security"></a>Windows Firewall con sicurezza avanzata  
  
1.  Nel Pannello di controllo di Windows 7 o Windows Vista fare clic su **Sistema e sicurezza**, selezionare **Windows Firewall**, quindi fare clic su **Impostazioni avanzate**. In Windows Server 2008 o 2008 R2 aprire Strumenti di amministrazione e fare clic su **Windows Firewall con protezione avanzata**. In Windows Server 2012 aprire la pagina Applicazioni e digitare **Windows Firewall**.  
  
2.  Per sbloccare l'accesso ad Analysis Services, fare clic con il pulsante destro del mouse su **Regole connessioni in entrata** , quindi scegliere **Nuova regola**.  
  
3.  In tipo di regola fare `Port` clic su Avanti e quindi su **Avanti**.  
  
4.  In Protocollo e porte selezionare **TCP** , quindi digitare la porta fissa in **Porte locali specifiche**.  
  
5.  In Azione fare clic su **Consenti la connessione** , quindi su **Avanti**.  
  
6.  In Profilo deselezionare tutti i percorsi di rete non applicabili, quindi fare clic su **Avanti**.  
  
7.  In nome digitare un nome descrittivo per questa regola (ad esempio, `SQL Server Analysis Services on port 54321`) e quindi fare clic su **fine**.  
  
8.  Per verificare che le connessioni remote siano abilitate, aprire SQL Server Management Studio o Excel in un computer diverso e connettersi al Analysis Services specificando il nome di rete del server e il numero di porta nel formato \<: nomeserver >: \<NumeroPorta >.  
  
#### <a name="netsh-advfirewall-syntax"></a>Sintassi di netsh advfirewall  
  
-   I comandi seguenti consentono di creare regole per le connessioni in entrata per sbloccare la porta TCP 2382 per il servizio SQL Server Browser e la porta fissa specificata per l'istanza di Analysis Services. È possibile eseguire uno qualsiasi dei due comandi per consentire l'accesso a un'istanza denominata di Analysis Services.  
  
     In questo comando di esempio, la porta fissa è la porta 54321. Sostituire il numero di porta con quello della porta effettivamente in uso nel sistema.  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> Utilizzare una porta fissa per un'istanza predefinita o denominata di Analysis Services  
 In questa sezione viene illustrato come configurare Analysis Services per l'ascolto su una porta fissa. L'utilizzo di una porta fissa è comune se Analysis Services è stato installato come istanza denominata, ma è inoltre possibile utilizzare questo approccio se i requisiti aziendali o di sicurezza specificano di utilizzare assegnazioni di porta non predefinite.  
  
 Si noti che l'utilizzo di una porta fissa implica la modifica della sintassi di connessione per l'istanza predefinita, in quanto è necessario aggiungere il numero di porta al nome del server. Per la connessione a un'istanza locale predefinita di Analysis Services in attesa sulla porta 54321 in SQL Server Management Studio, sarebbe ad esempio necessario digitare localhost:54321 come nome del server nella finestra di dialogo Connetti al server di Management Studio.  
  
 Se si utilizza un'istanza denominata, è possibile assegnare una porta fissa senza apportare alcuna modifica al modo in cui si specifica il nome del server (in particolare \<, è possibile utilizzare nomeserver\nomeistanza > per connettersi a un'istanza denominata in ascolto su una porta fissa). Tale operazione funziona solo se il servizio SQL Server Browser è in esecuzione ed è stata sbloccata la porta sulla quale è in attesa. SQL Server Browser servizio fornirà il reindirizzamento alla porta fissa basata su \<nomeserver\nomeistanza >. Se si aprono le porte sia per il servizio SQL Server Browser che per l'istanza denominata di Analysis Services in ascolto sulla porta fissa, tramite il servizio SQL Server Browser la connessione viene risolta in un'istanza denominata.  
  
1.  Determinare una porta TCP/IP disponibile da utilizzare.  
  
     Per visualizzare un elenco di porte riservate e registrate che è necessario evitare di usare, vedere la pagina relativa ai [numeri di porta (IANA)](https://go.microsoft.com/fwlink/?LinkID=198469). Per visualizzare un elenco di porte già in uso nel sistema, aprire una finestra del prompt dei comandi e digitare `netstat -a -p TCP` per visualizzare un elenco delle porte TCP aperte nel sistema.  
  
2.  Dopo aver determinato la porta da utilizzare, specificarla modificando l'impostazione di configurazione `Port` nel file msmdsrv.ini o nella pagina delle proprietà Generale di un'istanza di Analysis Services in SQL Server Management Studio.  
  
3.  Riavviare il servizio.  
  
4.  Configurare Windows Firewall per sbloccare la porta TCP specificata. In alternativa, se si sta utilizzando una porta fissa per un'istanza denominata, sbloccare sia la porta TCP specificata per tale istanza sia la porta TCP 2382 per il servizio SQL Server Browser.  
  
5.  Effettuare una verifica connettendosi localmente (in Management Studio) e, successivamente, in remoto da un'applicazione client in un altro computer. Per utilizzare Management Studio, connettersi a un'istanza predefinita di Analysis Services specificando il nome di un server nel \<formato nomeserver >\<: NumeroPorta >. Per un'istanza denominata, specificare il nome del server \<come NomeServer\\> <\>NomeIstanza.  
  
##  <a name="bkmk_cluster"></a> Configurazione delle porte per un cluster di Analysis Services  
 Un cluster di failover di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è sempre in ascolto sulla porta TCP 2383, indipendentemente da come è stato installato, istanza predefinita o denominata. Le assegnazioni di porta dinamiche non vengono utilizzate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se è installato in un cluster di failover Windows. Aprire TCP 2383 in ogni nodo con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione nel cluster. Per ulteriori informazioni sul clustering di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Come eseguire il clustering di SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548).  
  
##  <a name="bkmk_powerpivot"></a>Configurazione porta per PowerPivot per SharePoint  
 L'architettura server per [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] è fondamentalmente diversa a seconda della versione di SharePoint in uso.  
  
 **SharePoint 2013**  
  
 In SharePoint 2013, Excel Services reindirizza le richieste per i modelli di dati di PowerPivot, che vengono successivamente caricati in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'esterno dell'ambiente SharePoint. Le connessioni seguono il modello tipico, secondo cui da una libreria client di Analysis Services in un computer locale viene inviata una richiesta di connessione a un'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nella stessa rete.  
  
 Poiché con [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] viene sempre installato [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] come istanza denominata, considerare il servizio SQL Server Browser e le assegnazioni di porta dinamiche. Come già evidenziato, il servizio SQL Server Browser rimane in ascolto sulla porta TCP 2382 per le richieste di connessione inviate a istanze denominate di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , reindirizzando la richiesta alla porta corrente.  
  
 Si noti che in Excel Services in SharePoint 2013 non è supportata la sintassi di connessione alla porta fissa, quindi è opportuno assicurarsi che il servizio SQL Server Browser sia accessibile.  
  
 **SharePoint 2010**  
  
 Se si utilizza SharePoint 2010, non è necessario aprire le porte in Windows Firewall. In SharePoint vengono aperte le porte necessarie e i componenti aggiuntivi, ad esempio PowerPivot per SharePoint, vengono eseguiti nell'ambiente SharePoint. In un'installazione di PowerPivot per SharePoint 2010, il Servizio di sistema PowerPivot dispone dell'utilizzo esclusivo dell'istanza locale del servizio SQL Server Analysis Services (PowerPivot) installata nello stesso computer. Per l'accesso al servizio del motore Analysis Services locale, che consente operazioni di caricamento, esecuzione di query ed elaborazione di dati PowerPivot nel server SharePoint, vengono utilizzate connessioni locali e non di rete. Per richiedere dati PowerPivot da applicazioni client, le richieste vengono instradate tramite porte aperte dal programma di installazione di SharePoint. in particolare, vengono definite regole in ingresso per consentire l'accesso a SharePoint-80, amministrazione centrale SharePoint V4, servizi Web di SharePoint , e SPUserCodeV4). Poiché i servizi Web PowerPivot vengono eseguiti in una farm di SharePoint, le regole del firewall di SharePoint sono sufficienti per l'accesso remoto ai dati PowerPivot in una farm di SharePoint.  
  
## <a name="see-also"></a>Vedere anche  
 [Servizio SQL Server Browser &#40;motore di database e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
