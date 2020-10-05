---
title: Introduzione allo spazio dei nomi Microsoft.Data.SqlClient
description: Informazioni sullo spazio dei nomi Microsoft.Data.SqlClient e su come rappresenti il modo preferibile per connettersi ad applicazioni SQL per .NET.
ms.date: 09/29/2020
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: c3af23cb3816ad45fa75516633749d1f011c930d
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529352"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introduzione allo spazio dei nomi Microsoft.Data.SqlClient

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-20"></a>Note sulla versione per Microsoft.Data.SqlClient 2.0

Le note sulla versione sono disponibili anche nel repository GitHub: [Note sulla versione 2.0](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.0).

### <a name="breaking-changes"></a>Modifiche di rilievo

- Il modificatore di accesso per l'interfaccia del provider di enclave `SqlColumnEncryptionEnclaveProvider` è stato modificato da `public` a `internal`.

- Le costanti nella classe `SqlClientMetaDataCollectionNames` sono state aggiornate in modo da riflettere le modifiche apportate a SQL Server.

- Il driver eseguirà ora la convalida del certificato del server quando l'istanza di SQL Server di destinazione applica la crittografia TLS, che è l'impostazione predefinita per le connessioni di Azure.

- `SqlDataReader.GetSchemaTable()` restituisce ora una stringa `DataTable` vuota invece di `null`.

- Il driver esegue ora l'arrotondamento delle cifre decimali in modo che corrisponda al comportamento di SQL Server. Per la compatibilità con le versioni precedenti, è possibile abilitare il comportamento di troncamento precedente usando un'opzione di AppContext.

- Per le applicazioni .NET Framework che usano **Microsoft.Data.SqlClient**, i file SNI.dll scaricati in precedenza nelle cartelle `bin\x64` e `bin\x86` sono ora denominati `Microsoft.Data.SqlClient.SNI.x64.dll` e ` Microsoft.Data.SqlClient.SNI.x86.dll` e vengono scaricati nella directory `bin`.

- Nuovi sinonimi delle proprietà della stringa di connessione sostituiranno le proprietà obsolete durante il recupero della stringa di connessione da `SqlConnectionStringBuilder` per coerenza. [Altre informazioni](#new-connection-string-property-synonyms)

### <a name="new-features"></a>Nuove funzionalità

#### <a name="dns-failure-resiliency"></a>Resilienza agli errori DNS

Il driver memorizza ora nella cache gli indirizzi IP da ogni connessione riuscita a un endpoint SQL Server che supporta la funzionalità. Se si verifica un errore di risoluzione DNS durante un tentativo di connessione, il driver tenta di stabilire una connessione usando un indirizzo IP memorizzato nella cache per il server, se presente. 

#### <a name="eventsource-tracing"></a>Traccia EventSource

Questa versione introduce il supporto per l'acquisizione dei log di traccia eventi per il debug delle applicazioni. Per acquisire questi eventi, le applicazioni client devono restare in ascolto degli eventi dall'implementazione EventSource di SqlClient:

```
Microsoft.Data.SqlClient.EventSource
```

Per altre informazioni, vedere [Come abilitare la traccia eventi in SqlClient](enable-eventsource-tracing.md).

#### <a name="enabling-managed-networking-on-windows"></a>Abilitazione di reti gestite in Windows

Una nuova opzione di AppContext, **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** , consente l'uso di un'implementazione di SNI gestita in Windows per scopi di test e debug. Questa opzione attiva o disattiva il comportamento del driver in modo da usare uno SNI gestito in progetti .NET Core 2.1+ e .NET Standard 2.0+ in Windows, eliminando tutte le dipendenze dalle librerie native per la libreria Microsoft. Data.SqlClient.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

Per un elenco completo delle opzioni disponibili nel driver, vedere [Opzioni di AppContext in SqlClient](appcontext-switches.md).

#### <a name="enabling-decimal-truncation-behavior"></a>Abilitazione del comportamento di troncamento decimale 

Per impostazione predefinita, i dati decimali vengono arrotondati dal driver allo stesso modo che in SQL Server. Per la compatibilità con le versioni precedenti, è possibile impostare l'opzione di AppContext **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** su **true**.

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

#### <a name="new-connection-string-property-synonyms"></a>Nuovi sinonimi delle proprietà della stringa di connessione

Sono stati aggiunti nuovi sinonimi per le proprietà della stringa di connessione esistenti seguenti per evitare problemi di spaziatura tra le proprietà con più di una parola. I nomi di proprietà precedenti continueranno a essere supportati per la compatibilità con le versioni precedenti, ma le nuove proprietà della stringa di connessione verranno ora incluse durante il recupero della stringa di connessione da [SqlConnectionStringBuilder](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder).

|Proprietà della stringa di connessione esistente|Nuovo sinonimo|
|-----------------------------------|-----------|
| ApplicationIntent | Finalità dell'applicazione |
| ConnectRetryCount | Numero di tentativi di connessione |
| ConnectRetryInterval | Intervallo dei tentativi di connessione |
| PoolBlockingPeriod | Periodo di blocco del pool |
| MultipleActiveResultSets | Più set di risultati attivi |
| MultiSubnetFailover | Failover di più subnet |
| TransparentNetworkIPResolution | Risoluzione dell'IP di rete trasparente |
| TrustServerCertificate | TrustServerCertificate |

#### <a name="sqlbulkcopy-rowscopied-property"></a>Proprietà RowsCopied di SqlBulkCopy

La proprietà RowsCopied fornisce accesso in sola lettura al numero di righe elaborate durante l'operazione di copia bulk in corso. Questo valore non deve necessariamente essere uguale al numero finale di righe aggiunte alla tabella di destinazione. 

#### <a name="connection-open-overrides"></a>Override dell'apertura della connessione

È possibile eseguire l'override del comportamento predefinito di SqlConnection.Open() per disabilitare il ritardo di dieci secondi e i tentativi di connessione automatici attivati da errori temporanei.

```csharp
using SqlConnection sqlConnection = new SqlConnection("Data Source=(local);Integrated Security=true;Initial Catalog=AdventureWorks;");
sqlConnection.Open(SqlConnectionOverrides.OpenWithoutRetry);
```

> [!NOTE]
> Si noti che questo override può essere applicato solo a SqlConnection.Open() e non a SqlConnection.OpenAsync().

#### <a name="username-support-for-active-directory-interactive-mode"></a>Supporto di nomi utente per la modalità interattiva di Azure Active Directory

È possibile specificare un nome utente nella stringa di connessione quando si usa la modalità di autenticazione interattiva di Azure Active Directory per .NET Framework e .NET Core

Impostare un nome utente usando la proprietà **User ID** o **UID** della stringa di connessione:

```
"Server=<server name>; Database=<db name>; Authentication=Active Directory Interactive; User Id=<username>;"
```

#### <a name="order-hints-for-sqlbulkcopy"></a>Suggerimenti per l'ordinamento per SqlBulkCopy

È possibile fornire suggerimenti per l'ordinamento per migliorare le prestazioni delle operazioni di copia bulk sulle tabelle con indici cluster. Per altre informazioni, vedere la sezione [Operazioni di copia bulk](sql/bulk-copy-order-hints.md).

#### <a name="sni-dependency-changes"></a>Modifiche alle dipendenze di SNI

Microsoft.Data.SqlClient (.NET Core e .NET Standard) in Windows è ora dipendente da **Microsoft.Data.SqlClient.SNI.runtime**, in sostituzione alla precedente dipendenza da **runtime.native.System.Data.SqlClient.SNI**. La nuova dipendenza aggiunge il supporto per la piattaforma ARM insieme alle piattaforme già supportate ARM64, x64 e x86 in Windows.

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Note sulla versione per Microsoft.Data.SqlClient 1.1.0

Le note sulla versione sono disponibili anche nel repository GitHub: [Note sulla versione 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Nuove funzionalità

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclave sicuri

Always Encrypted è disponibile a partire da Microsoft SQL Server 2016. Gli enclave sicuri sono disponibili a partire da Microsoft SQL Server 2019. Per usare la funzionalità di enclave, le stringhe di connessione devono includere il protocollo di attestazione e l'URL di attestazione necessari. Ad esempio:

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

Per altre informazioni, vedere:

- [Supporto di SqlClient per Always Encrypted](sql/sqlclient-support-always-encrypted.md)
- [Esercitazione: Sviluppare un'applicazione .NET usando Always Encrypted con enclave sicure](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Note sulla versione per Microsoft.Data.SqlClient 1.0

La versione iniziale dello spazio dei nomi Microsoft.Data.SqlClient offre funzionalità aggiuntive rispetto allo spazio dei nomi System.Data.SqlClient esistente.
Le note sulla versione sono disponibili anche nel repository GitHub: [Note sulla versione 1.0](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0).

### <a name="new-features"></a>Nuove funzionalità

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Nuove funzionalità rispetto a .NET Framework 4.7.2 System.Data.SqlClient

- **Classificazione dei dati**: disponibile nel database SQL di Azure e in Microsoft SQL Server 2019.

- **Supporto UTF-8**: disponibile in Microsoft SQL Server 2019.

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Nuove funzionalità rispetto a .NET Core 2.2 System.Data.SqlClient

- **Classificazione dei dati**: disponibile nel database SQL di Azure e in Microsoft SQL Server 2019.

- **Supporto UTF-8**: disponibile in Microsoft SQL Server 2019.

- **Autenticazione**: modalità di autenticazione con password di Active Directory.

### <a name="data-classification"></a>Classificazione dei dati

La classificazione dei dati offre un nuovo set di API che espongono informazioni di sola lettura sulla riservatezza e classificazione dei dati relative agli oggetti recuperati tramite SqlDataReader quando l'origine sottostante supporta la funzionalità e contiene metadati di [riservatezza e classificazione dei dati](../../relational-databases/security/sql-data-discovery-and-classification.md). Vedere l'applicazione di esempio in [Data Discovery and Classification in SqlClient](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>Supporto UTF-8

Il supporto UTF-8 non richiede modifiche al codice dell'applicazione. Queste modifiche di SqlClient consentono di ottimizzare la comunicazione tra il client e il server quando il server supporta UTF-8 e le regole di confronto delle colonne sottostanti usano UTF-8. Vedere la sezione UTF-8 in [Novità di SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted con enclave

In generale, la documentazione esistente che usa System.Data.SqlClient in .NET Framework **e i provider dell'archivio chiavi master delle colonne predefiniti** può ora essere usata anche con .NET Core.

 [Sviluppare con Always Encrypted e il provider di dati .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: proteggere i dati sensibili e archiviare le chiavi di crittografia nell'archivio certificati di Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Authentication

È possibile specificare modalità di autenticazione diverse usando l'opzione della stringa di connessione _Authentication_. Per altre informazioni, vedere la [documentazione di SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> I provider dell'archivio chiavi personalizzati, come il provider Azure Key Vault, dovranno essere aggiornati per supportare Microsoft.Data.SqlClient. In modo analogo, anche i provider di enclave dovranno essere aggiornati per supportare Microsoft.Data.SqlClient.
> Always Encrypted è supportato solo su destinazioni .NET Framework e .NET Core. Non è supportato su .NET Standard perché in .NET Standard mancano alcune dipendenze di crittografia.
