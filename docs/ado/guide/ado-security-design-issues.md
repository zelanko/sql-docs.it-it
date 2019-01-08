---
title: Problemi di progettazione della protezione ADO | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a879e05e5c2df68058d9351b217382366ae80a0d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532355"
---
# <a name="ado-security-design-features"></a>Funzionalità di progettazione della protezione di ADO
Le sezioni seguenti descrivono le funzionalità di progettazione di sicurezza in oggetti ADO (ActiveX Data) 2.8 e versioni successive. Queste modifiche sono state apportate per migliorare la sicurezza ADO 2.8. ADO 6.0, che è incluso in Windows DAC 6.0 in Windows Vista, è funzionalmente equivalente a ADO 2.8, che è stato incluso in MDAC 2.8 in Windows XP e Windows Server 2003. In questo argomento fornisce informazioni su come proteggere meglio le applicazioni ADO 2.8 o successiva.

> [!IMPORTANT]
>  Se si sta aggiornando l'applicazione da una versione precedente di ADO, è consigliabile testare l'applicazione aggiornata in un computer non di produzione prima di distribuirlo ai clienti. In questo modo, è possibile assicurarsi che si è a conoscenza di eventuali problemi di compatibilità prima di distribuire l'applicazione aggiornata.

## <a name="internet-explorer-file-access-scenarios"></a>Scenari di accesso File di Internet Explorer
 L'effetto seguente funzionalità come ADO 2.8 e versioni successiva funziona quando viene usata inserito nello script le pagine Web in Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Finestra di messaggio di avviso rivista e migliorata sicurezza ora utilizzato per avvertire gli utenti
 Per ADO 2.7 e versioni precedente, il seguente messaggio di avviso viene visualizzato quando una pagina Web con script tenta di eseguire il codice ADO da un provider non attendibile:

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Per ADO 2.8 e versioni successiva, il messaggio riportato sopra sia scomparsa. In alternativa, in questo contesto viene visualizzato il messaggio seguente:

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 Il messaggio riportato sopra consente all'utente di prendere decisioni informate, sapendo le conseguenze per entrambe le opzioni:

-   Se l'utente di trust tra il sito, fare clic su OK consentirà tutto il codice indipendente dai disco (tutti i metodi e proprietà ADO con le eccezioni delle API accessibile da disco descritte più avanti in questo argomento) per eseguire ed eseguire nella finestra del browser.

-   Se l'utente non considera attendibile il sito, facendo clic su Annulla blocca il codice ADO per accedere ai dati da in esecuzione e l'esecuzione nel suo complesso.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Codice accessibile da disco, limitato a questo punto per siti attendibili
 Sono state apportate modifiche di Progettazione aggiuntive in ADO 2.8 che limitano l'utilizzo in modo specifico la capacità di un set limitato di API, che potrebbero esporre la possibilità di leggere o scrivere file nel computer locale. Ecco i metodi dell'API che sono stati ulteriormente limitate per motivi di sicurezza durante l'esecuzione di Internet Explorer:

-   Per l'oggetto ADO **Stream** dell'oggetto, se il [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) oppure [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) vengono usati i metodi.

-   Per l'oggetto ADO **Recordset** dell'oggetto, se il valore il [salvare](../../ado/reference/ado-api/save-method.md) (metodo) o il [Open](../../ado/reference/ado-api/open-method-ado-recordset.md) metodo, ad esempio, quando entrambi il **adCmdFile** opzione è impostata o il [Provider Microsoft OLE DB Persistence (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) viene usato.

 Per questi set limitato di funzioni potenzialmente accessibile da disco, si verifica quanto segue per ADO 2.8 e versioni successiva, se qualsiasi codice che usa questi metodi viene eseguito in Internet Explorer:

-   Se il sito che ha fornito il codice è stato già aggiunto all'elenco di zona siti attendibili, il codice viene eseguito nel browser e accedere ai file locali.

-   Se il sito non viene visualizzato nell'elenco a discesa zona siti attendibili, il codice viene bloccato e viene negato l'accesso ai file locali.

    > [!NOTE]
    >  In ADO 2.8 e versioni successiva, l'utente non è un avviso o è consigliabile aggiungere i siti all'elenco di zona siti attendibili. La gestione dell'elenco dei siti attendibili è pertanto la responsabilità di chi distribuzione o il supporto di applicazioni basato su sito Web che richiedono l'accesso al file system locale.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Accesso bloccato alla proprietà ActiveCommand sugli oggetti di Recordset
 Quando si esegue Internet Explorer, ADO 2.8 ora blocca l'accesso per il [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) proprietà per un oggetto attivo **Recordset** specificato e restituisce un errore. L'errore si verifica indipendentemente dal fatto che la pagina deriva da un sito Web registrato nell'elenco dei siti attendibili.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Novità di gestione per i provider OLE DB e la sicurezza integrata
 Quando si esamina ADO 2.7 e versioni precedenti per potenziali problemi e problemi di sicurezza, è stato individuato lo scenario seguente:

 In alcuni casi, i provider OLE DB che supportano la sicurezza integrata [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) proprietà potenzialmente potrebbe consentire l'utilizzo con script alle pagine Web di riutilizzare l'oggetto connessione ADO per connettersi inavvertitamente in altri server usando le credenziali di account di accesso corrente degli utenti. Per evitare questo problema, ADO 2.8 e versioni successiva gestiscono i provider OLE DB a seconda del modo in cui si è scelto di fornire o non forniscono, per la sicurezza integrata.

 Web Pages caricati da siti elencati nell'elenco a discesa zona siti attendibili, la tabella seguente fornisce un riepilogo delle modalità di gestione delle connessioni ADO in ogni caso ADO 2.8 e versioni successiva.

|Impostazioni di Internet Explorer per l'autenticazione utente, l'accesso|Supporta provider "Integrated Security" e UID e PWD vengono specificati (SQLOLEDB)|Il provider non supporta "Integrated Security" (JOLT, MSDASQL, MSPersist)|Provider supporta "Integrated Security" ed è impostato su SSPI (nessun UID/PWD vengono specificati)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Accesso automatico con nome utente corrente e la password|Consenti la connessione|Consenti la connessione|Consenti la connessione|
|Richiedi nome utente e password|Consenti la connessione|Connessione ha esito negativo|Connessione ha esito negativo|
|Accesso automatico solo nell'area Intranet|Consenti la connessione|Richiedere all'utente un avviso di protezione|Richiedere all'utente un avviso di protezione|
|Accesso anonimo|Consenti la connessione|Connessione ha esito negativo|Connessione ha esito negativo|

 Nel caso in cui viene visualizzato un avviso di sicurezza a questo punto, la finestra di messaggio informa l'utente:

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 Il messaggio riportato sopra consente all'utente di prendere una decisione più oculata e procedere di conseguenza.

> [!NOTE]
>  Per i siti non attendibili (ovvero, i siti non elencati nell'elenco a discesa zona siti attendibili), se il provider viene anche non attendibile (come indicato in precedenza in questa sezione), l'utente potrebbe visualizzare due avvisi di sicurezza in una riga, un avviso sul provider di tipo unsafe e un secondo messaggio di avviso Provare a usare la propria identità. Se l'utente fa clic su OK per il primo avviso, vengono eseguite le impostazioni di Internet Explorer e un codice di risposta del comportamento descritto nella tabella precedente.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controllare se viene restituito il testo della password nelle stringhe di connessione ADO
 Quando si tenta di ottenere il valore della [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà in un oggetto ADO **connessione** dell'oggetto, si verificano gli eventi seguenti:

1.  Se la connessione è aperta, una chiamata di inizializzazione viene quindi inviata al provider OLE DB sottostante per ottenere la stringa di connessione.

2.  A seconda dell'impostazione nel provider OLE DB del [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) proprietà, le password sono incluse insieme alle altre informazioni sulla stringa di connessione che viene restituiti.

 Ad esempio, se la proprietà dinamica ADO Connection **Persist Security Info** è impostata su **True**, le informazioni sulla password è incluso nella stringa di connessione restituita. In caso contrario, se il provider sottostante ha impostato la proprietà **False** (ad esempio con il provider SQLOLEDB), le informazioni sulla password viene omessa nella stringa di connessione restituito.

 Se si usa terze parti (vale a dire non Microsoft) provider OLE DB con il codice dell'applicazione ADO, è possibile controllare come la **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** proprietà viene implementata per determinare se inclusione di le informazioni sulla password con le stringhe di connessione ADO è consentiti.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Verifica per i dispositivi non basati su file durante il caricamento e salvataggio di recordset o flussi
 Per ADO 2.7 e versioni precedente, file di operazioni di input/output, ad esempio [aperto](../../ado/reference/ado-api/open-method-ado-recordset.md) e [salvare](../../ado/reference/ado-api/save-method.md) che sono stati usati per leggere e scrivere i dati basati su file potrebbe consentire in alcuni casi un nome file o URL da usare che specificare un diverso da un disco basa il tipo di file. Ad esempio, LPT1, COM2, PRN. TXT, AUX potrebbe essere utilizzato come alias per l'input/output tra le stampanti e ausiliari dispositivi nel sistema usando determinati

 Per ADO 2.8 e versioni successiva, questa funzionalità è stata aggiornata. Per l'apertura e salvataggio **Recordset** e **Stream** gli oggetti ADO esegue ora un controllo del tipo di file per assicurarsi che il dispositivo di input o output specificato in un URL o nel nome file sia un file effettivo.

> [!NOTE]
>  Controllo dei tipi di file come descritto in questa sezione si applica solo per Windows 2000 e versioni successive. Non è applicabile a situazioni in cui ADO 2.8 o versione successiva è in esecuzione con le versioni precedenti di Windows, ad esempio Windows 98.
