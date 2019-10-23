---
title: Introduzione allo spazio dei nomi Microsoft.Data.SqlClient
description: Pagina introduttiva per lo spazio dei nomi Microsoft. Data. SqlClient.
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452387"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Introduzione allo spazio dei nomi Microsoft.Data.SqlClient

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Scaricare ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Questa pagina descrive il modo in cui lo spazio dei nomi Microsoft. Data. SqlClient offre funzionalità aggiuntive sullo spazio dei nomi System. Data. SqlClient esistente.
  
## <a name="release-notes"></a>Note sulla versione
Tutte le note sulla versione sono disponibili nel [repository GitHub](https://github.com/dotnet/SqlClient/tree/master/release-notes).

## <a name="new-features"></a>Nuove funzionalità

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>Nuove funzionalità rispetto a .NET Framework 4.7.2 System. Data. SqlClient

Classificazione dei dati: disponibile nel database SQL di Azure e Microsoft SQL Server 2019 dalla versione CTP 2,0.

Supporto per UTF-8-disponibile in Microsoft SQL Server SQL Server 2019 dalla versione CTP 2,3.

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>Nuove funzionalità rispetto a .NET Core 2,2 System. Data. SqlClient

Classificazione dei dati: disponibile nel database SQL di Azure e Microsoft SQL Server 2019 dalla versione CTP 2,0.

Supporto per UTF-8-disponibile in Microsoft SQL Server SQL Server 2019 dalla versione CTP 2,3.

Always Encrypted con enclave-Always Encrypted è disponibile Microsoft SQL Server 2016 e versioni successive. Il supporto per l'enclave è stato introdotto in Microsoft SQL Server 2019 CTP 2,0.

Autenticazione-Active Directory modalità di autenticazione della password.

### <a name="data-classification"></a>Classificazione dei dati

Classificazione dei dati offre un nuovo set di API che espongono le informazioni di classificazione e la riservatezza dei dati di sola lettura sugli oggetti recuperati tramite SqlDataReader quando l'origine sottostante supporta la funzionalità e contiene metadati sulla [sensibilità dei dati e classificazione](../../relational-databases/security/sql-data-discovery-and-classification.md).

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

Il supporto UTF-8 non richiede alcuna modifica del codice dell'applicazione. Queste modifiche SqlClient consentono semplicemente di ottimizzare la comunicazione tra il client e il server quando il server supporta UTF-8 e le regole di confronto delle colonne sottostanti sono UTF-8. Vedere la sezione UTF-8 in [What ' s New in SQL Server 2019 Preview](../../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="always-encrypted-with-enclaves"></a>Crittografia sempre attiva con enclave

In generale, la documentazione esistente che usa System. Data. SqlClient su .NET Framework **e i provider dell'archivio chiavi master della colonna predefiniti** dovrebbero ora funzionare anche con .NET Core.

 [Sviluppare con Always Encrypted e il provider di dati .NET Framework](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted: proteggere i dati sensibili e archiviare le chiavi di crittografia nell'archivio certificati di Windows](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>Autenticazione

È possibile specificare diverse modalità di autenticazione usando l'opzione della stringa di connessione per l' _autenticazione_ . Per ulteriori informazioni, vedere la [documentazione relativa a SqlAuthenticationMethod](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2).

> [!NOTE]
> I provider di archivio chiavi personalizzati, come il provider di Azure Key Vault, dovranno essere aggiornati per supportare Microsoft. Data. SqlClient. Analogamente, anche i provider di enclave dovranno essere aggiornati per supportare Microsoft. Data. SqlClient.
> Always Encrypted è supportato solo per le destinazioni .NET Framework e .NET Core. Non è supportata per .NET Standard perché .NET Standard mancano determinate dipendenze di crittografia.
