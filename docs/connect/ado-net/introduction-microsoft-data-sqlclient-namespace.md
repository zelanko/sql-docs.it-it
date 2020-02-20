---
title: Introduzione allo spazio dei nomi Microsoft.Data.SqlClient
description: Pagina di introduzione per lo spazio dei nomi Microsoft.Data.SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e64a4b04e5059ebc4acbd8e673746fc3953fbb03
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251000"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introduzione allo spazio dei nomi Microsoft.Data.SqlClient

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Scaricare ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Note sulla versione per Microsoft.Data.SqlClient 1.1.0

Le note sulla versione sono disponibili anche nel repository GitHub: [Note sulla versione 1.1](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1).

### <a name="new-features"></a>Nuove funzionalità

#### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclave sicuri

Always Encrypted è disponibile a partire da Microsoft SQL Server 2016. Gli enclave sicuri sono disponibili a partire da Microsoft SQL Server 2019. Per usare la funzionalità di enclave, le stringhe di connessione devono includere il protocollo di attestazione e l'URL di attestazione necessari. Esempi:

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

Per informazioni dettagliate, vedere:

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

La classificazione dei dati offre un nuovo set di API che espongono informazioni di sola lettura sulla riservatezza e classificazione dei dati relative agli oggetti recuperati tramite SqlDataReader quando l'origine sottostante supporta la funzionalità e contiene metadati di [riservatezza e classificazione dei dati](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

Il supporto UTF-8 non richiede modifiche al codice dell'applicazione. Queste modifiche di SqlClient consentono semplicemente di ottimizzare la comunicazione tra il client e il server quando il server supporta UTF-8 e le regole di confronto delle colonne sottostanti usano UTF-8. Vedere la sezione UTF-8 in [Novità di SQL Server 2019 (anteprima)](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Always Encrypted con enclave

In generale, la documentazione esistente che usa System.Data.SqlClient in .NET Framework **e i provider dell'archivio chiavi master delle colonne predefiniti** può ora essere usata anche con .NET Core.

 [Sviluppare con Always Encrypted e il provider di dati .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: proteggere i dati sensibili e archiviare le chiavi di crittografia nell'archivio certificati di Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Authentication

È possibile specificare modalità di autenticazione diverse usando l'opzione della stringa di connessione _Authentication_. Per altre informazioni, vedere la [documentazione di SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> I provider dell'archivio chiavi personalizzati, come il provider Azure Key Vault, dovranno essere aggiornati per supportare Microsoft.Data.SqlClient. In modo analogo, anche i provider di enclave dovranno essere aggiornati per supportare Microsoft.Data.SqlClient.
> Always Encrypted è supportato solo su destinazioni .NET Framework e .NET Core. Non è supportato su .NET Standard perché in .NET Standard mancano alcune dipendenze di crittografia.
