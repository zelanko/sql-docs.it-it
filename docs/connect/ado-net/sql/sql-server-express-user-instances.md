---
title: Istanze utente di SQL Server Express
description: Viene descritto il supporto per SQL Server Express istanze utente.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452017"
---
# <a name="sql-server-express-user-instances"></a>Istanze utente di SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) supporta la funzionalità dell'istanza utente, disponibile solo quando si utilizza il provider di dati Microsoft SqlClient per SQL Server. Un'istanza utente è un'istanza separata del SQL Server Express motore di database generata da un'istanza padre. Le istanze utente consentono agli utenti che non sono amministratori dei computer locali di collegarsi e connettersi ai database SQL Server Express. Ogni istanza viene eseguita nel contesto di sicurezza del singolo utente, in base a una sola istanza per singolo utente.  
  
## <a name="user-instance-capabilities"></a>Funzionalità dell'istanza utente  
Le istanze utente sono utili per gli utenti che eseguono Windows con un account utente con privilegi minimi, perché ogni utente dispone di privilegi SQL Server amministratore di sistema (`sysadmin`) sull'istanza in esecuzione nel computer senza che sia necessario eseguirla come Windows anche l'amministratore. Il software in esecuzione in un'istanza utente con autorizzazioni limitate non può apportare modifiche a livello di sistema perché l'istanza di SQL Server Express viene eseguita con l'account di Windows non amministratore dell'utente e non come servizio. Ogni istanza utente è isolata dall'istanza padre e da qualsiasi altra istanza utente eseguita nello stesso computer. I database in esecuzione in un'istanza utente vengono aperti solo in modalità utente singolo e non è possibile che più utenti si connettano ai database in esecuzione in un'istanza utente. Anche la replica e le query distribuite sono disabilitate per le istanze utente.  
  
Per altre informazioni, vedere "Istanze utente" nella documentazione online di SQL Server.  
  
> [!NOTE]
>  Le istanze utente non sono necessarie per gli utenti che sono già amministratori nei propri computer o per gli scenari che coinvolgono più utenti del database.  
  
## <a name="enabling-user-instances"></a>Abilitazione di istanze utente  
Per generare istanze utente, è necessario che sia in esecuzione un'istanza padre di SQL Server Express. Le istanze utente vengono abilitate per impostazione predefinita durante l'installazione di SQL Server Express e possono essere abilitate o disabilitate in modo esplicito da un amministratore di sistema eseguendo la stored procedure **sp_configure** sull'istanza padre.  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
Il protocollo di rete per le istanze utente deve essere Named Pipes locale. Non è possibile avviare un'istanza utente in un'istanza remota di SQL Server e SQL Server account di accesso non sono consentiti.  
  
## <a name="connecting-to-a-user-instance"></a>Connessione a un'istanza utente  
Le parole chiave `User Instance` e `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> consentono la connessione di <xref:Microsoft.Data.SqlClient.SqlConnection> a un'istanza utente. Le istanze utente sono supportate anche dalle proprietà <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` e `AttachDBFilename`.  
  
Si noti quanto segue sulla stringa di connessione di esempio illustrata di seguito:  
  
- La parola chiave `Data Source` fa riferimento all'istanza padre di SQL Server Express che genera l'istanza utente. L'istanza predefinita è .\SQLEXPRESS.  
  
- `Integrated Security` è impostato su `true`. Per connettersi a un'istanza utente, è necessaria l'autenticazione di Windows. Gli account di accesso SQL Server non sono supportati.  
  
- Il `User Instance` è impostato su `true`, che richiama un'istanza utente. (Il valore predefinito è `false`.)  
  
- La parola chiave della stringa di connessione `AttachDbFileName` viene utilizzata per collegare il file di database primario (con estensione MDF), che deve includere il nome del percorso completo. `AttachDbFileName` corrisponde anche alle chiavi "Extended Properties" e "Initial file name" all'interno di una stringa di connessione <xref:Microsoft.Data.SqlClient.SqlConnection>.  
  
- La stringa di sostituzione `|DataDirectory|` racchiusa tra i simboli della pipe si riferisce alla directory dei dati dell'applicazione che apre la connessione e fornisce un percorso relativo che indica il percorso dei file di database e di log con estensione MDF e ldf. Se si desidera trovare questi file altrove, è necessario specificare il percorso completo dei file.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  Per compilare una stringa di connessione in fase di esecuzione, è anche possibile usare le proprietà <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> e <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A>.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>Utilizzo della &#124;stringa di&#124; sostituzione DataDirectory  
`DataDirectory` viene usata insieme a `AttachDbFileName` per indicare un percorso relativo di un file di dati, consentendo agli sviluppatori di creare stringhe di connessione basate su un percorso relativo dell'origine dati senza che sia necessario specificare un percorso completo.  
  
Il percorso fisico a cui `DataDirectory` punta dipende dal tipo di applicazione. In questo esempio il file Northwind. MDF da collegare si trova nella cartella \app_data dell'applicazione.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
Quando si utilizza `DataDirectory`, il percorso del file risultante non può essere superiore nella struttura di directory rispetto alla directory a cui fa riferimento la stringa di sostituzione. Se, ad esempio, il `DataDirectory` completamente espanso è C:\AppDirectory\app_data, la stringa di connessione di esempio illustrata sopra funziona perché è sotto c:\AppDirectory. Se tuttavia si tenta di specificare `DataDirectory` come `|DataDirectory|\..\data`, verrà generato un errore perché \data non è una sottodirectory di \AppDirectory.  
  
Se la stringa di connessione contiene una stringa di sostituzione formattata in modo non corretto, verrà generata un'<xref:System.ArgumentException>.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient> risolve le stringhe di sostituzione in percorsi completi rispetto al file system del computer locale. Pertanto, i nomi di percorso server remoto, HTTP e UNC non sono supportati. Quando la connessione viene aperta, viene generata un'eccezione se il server non si trova nel computer locale.  
  
Quando il <xref:Microsoft.Data.SqlClient.SqlConnection> viene aperto, viene reindirizzato dall'istanza predefinita di SQL Server Express a un'istanza avviata in fase di esecuzione in esecuzione con l'account del chiamante.  
  
> [!NOTE]
>  Potrebbe essere necessario aumentare il valore di <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> poiché le istanze utente potrebbero richiedere più tempo per il caricamento delle istanze normali.  
  
Il frammento di codice seguente apre un nuovo `SqlConnection`, Visualizza la stringa di connessione nella finestra della console e quindi chiude la connessione quando si esce dal blocco di codice `using`.  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  Le istanze utente non sono supportate nel codice Common Language Runtime (CLR) eseguito all'interno di SQL Server. Viene generata un'<xref:System.InvalidOperationException> se viene chiamato `Open` su un <xref:Microsoft.Data.SqlClient.SqlConnection> con `User Instance=true` nella stringa di connessione.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>Durata di una connessione a un'istanza utente  
Diversamente dalle versioni di SQL Server eseguite come servizio, non è necessario avviare e arrestare manualmente le istanze di SQL Server Express. Ogni volta che un utente esegue l'accesso e si connette a un'istanza utente, l'istanza utente viene avviata se non è già in esecuzione. Per i database dell'istanza utente è impostata l'opzione `AutoClose`, in modo che il database venga arrestato automaticamente dopo un periodo di inattività. Il processo sqlservr. exe avviato viene mantenuto in esecuzione per un periodo di timeout limitato dopo la chiusura dell'ultima connessione all'istanza, pertanto non è necessario riavviarlo se viene aperta un'altra connessione prima della scadenza del timeout. L'istanza utente viene arrestata automaticamente se non viene aperta alcuna nuova connessione prima della scadenza del periodo di timeout. Un amministratore di sistema dell'istanza padre può impostare la durata del periodo di timeout per un'istanza utente usando **sp_configure** per modificare l'opzione **user instance timeout**. Il valore predefinito è 60 minuti.  
  
> [!NOTE]
>  Se `Min Pool Size` viene utilizzata nella stringa di connessione con un valore maggiore di zero, il pool di connessione manterrà sempre alcune connessioni aperte e l'istanza utente non verrà arrestata automaticamente.  
  
## <a name="how-user-instances-work"></a>Funzionamento delle istanze utente  
La prima volta che viene generata un'istanza utente per ogni utente, i database di sistema **master** e **msdb** vengono copiati dalla cartella Template Data in un percorso all'interno della directory di repository dei dati dell'applicazione locale dell'utente per l'uso esclusivo da parte dell'istanza utente. Questo percorso è in genere `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`. Quando un'istanza utente viene avviata, in questa directory vengono scritti anche i file **tempdb**, di log e di traccia. Viene generato un nome per l'istanza di, che è sicuramente univoco per ogni utente.  
  
Per impostazione predefinita, a tutti i membri del gruppo Builtin\Users di Windows vengono concesse le autorizzazioni per connettersi all'istanza locale, nonché le autorizzazioni di lettura ed esecuzione per i file binari SQL Server. Una volta verificate le credenziali dell'utente chiamante che ospita l'istanza utente, tale utente diventa il `sysadmin` su tale istanza. Per le istanze utente è abilitata solo la memoria condivisa, il che significa che sono possibili solo le operazioni nel computer locale.  
  
È necessario concedere agli utenti le autorizzazioni di lettura e scrittura per i file con estensione MDF e ldf specificati nella stringa di connessione.  
  
> [!NOTE]
>  I file con estensione MDF e ldf rappresentano rispettivamente i file di database e di log. Questi due file sono un set di corrispondenze, pertanto è necessario prestare attenzione durante le operazioni di backup e ripristino. Il file di database contiene informazioni sulla versione esatta del file di log e il database non verrà aperto se è associato a un file di log errato.  
  
Per evitare il danneggiamento dei dati, viene aperto un database nell'istanza utente con accesso esclusivo. Se due istanze utente diverse condividono lo stesso database nello stesso computer, è necessario che l'utente nella prima istanza chiuda il database prima di poterlo aprire in una seconda istanza.  
  
## <a name="user-instance-scenarios"></a>Scenari di istanze utente  
Le istanze utente forniscono agli sviluppatori di applicazioni di database un archivio dati di SQL Server che non dipende dagli sviluppatori che dispongono di account amministrativi nei propri computer di sviluppo. Le istanze utente sono basate sul modello di accesso/Jet, in cui l'applicazione di database si connette semplicemente a un file e l'utente dispone automaticamente delle autorizzazioni complete su tutti gli oggetti di database senza che sia necessario l'intervento di un amministratore di sistema per concedere autorizzazioni. È progettato per funzionare in situazioni in cui l'utente è in esecuzione con un account utente con privilegi minimi e non dispone di privilegi amministrativi nel server o nel computer locale, ma è necessario creare oggetti di database e applicazioni. Le istanze utente consentono agli utenti di creare istanze in fase di esecuzione eseguite nel contesto di sicurezza dell'utente e non nel contesto di sicurezza di un servizio di sistema con privilegi più elevati.  
  
> [!IMPORTANT]
>  Le istanze utente devono essere utilizzate solo negli scenari in cui tutte le applicazioni che lo utilizzano sono completamente attendibili.  
  
Gli scenari di istanze utente includono:  
  
- Qualsiasi applicazione a singolo utente in cui non è necessario condividere i dati.  
  
- Distribuzione ClickOnce. Se .NET Framework 2.0 (o versioni successive) o .NET Core 1.0 (o versioni successive) e SQL Server Express sono già installati nel computer di destinazione, il pacchetto di installazione scaricato come risultato di un'azione ClickOnce può essere installato e usato da utenti non amministratori. Si noti che un amministratore deve installare SQL Server Express se fa parte dell'installazione di. Per ulteriori informazioni, vedere [la pagina relativa alla distribuzione ClickOnce per Windows Forms](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms).
  
- Hosting ASP.NET dedicato con autenticazione di Windows. Una singola istanza di SQL Server Express può essere ospitata in una rete Intranet. L'applicazione si connette utilizzando l'account di Windows ASPNET, non utilizzando la rappresentazione. Le istanze utente non devono essere usate per scenari di hosting condiviso o di terze parti in cui tutte le applicazioni condividono la stessa istanza utente e non rimarranno più isolate l'una dall'altra.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
