---
title: Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/06/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26402f5b15fa7dd8e24b13f3adc41836ff275228
ms.sourcegitcommit: c61c7b598aa61faa34cd802697adf3a224aa7dc4
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56154686"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo elenca le librerie che dipende da Microsoft JDBC Driver per SQL Server. Il progetto contiene le dipendenze seguenti.

## <a name="compile-time"></a>Fase di compilazione

 - `com.microsoft.azure:azure-keyvault` : Azure Key Vault Provider per la funzionalità Always Encrypted Azure Key Vault (facoltativa)
 - `com.microsoft.azure:azure-keyvault-webkey` : Azure Key Vault Provider per la funzionalità Always Encrypted Azure Key Vault (facoltativa)
 - `com.microsoft.azure:adal4j` : Azure Active Directory Library for Java per la funzionalità di autenticazione di Azure Active Directory e funzionalità di Azure Key Vault (facoltativa)
 - `com.microsoft.rest:client-runtime` : Azure Active Directory Library for Java per la funzionalità di autenticazione di Azure Active Directory e funzionalità di Azure Key Vault (facoltativa)
- `org.osgi:org.osgi.core`: Libreria principale di OSGi per supporto OSGi Framework.
- `org.osgi:org.osgi.compendium`: Libreria Compendium OSGi per supporto OSGi Framework.

## <a name="test-time"></a>Tempo test

È necessario dichiarare in modo esplicito le rispettive dipendenze nel file POM progetti specifici che richiedono una funzionalità precedente.

**Ad esempio:** quando si usa la funzionalità di autenticazione di Azure Active Directory, è necessario dichiarare di nuovo il `adal4j` dipendenza nel file POM del progetto. Vedere il frammento seguente:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>
```

**Ad esempio:** quando si usa la funzionalità Azure Key Vault, è necessario dichiarare di nuovo il `azure-keyvault` dipendenza e `adal4j` dipendenza nel file POM del progetto. Vedere il frammento seguente:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.2.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.3</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.5</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.0</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault-webkey</artifactId>
    <version>1.2.0</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisiti di dipendenza per il driver JDBC

### <a name="working-with-the-azure-key-vault-provider"></a>Uso del Provider di Azure Key Vault:

- Microsoft JDBC Driver versione 7.2.1 - le versioni delle dipendenze: Azure-Keyvault (versione 1.2.0), Azure-Keyvault-Webkey (versione 1.2.0) e Adal4j (versione 1.6.3), Client-Runtime-per-AutoRest (1.6.5) e le relative dipendenze ([applicazionediesempio](../../connect/jdbc/azure-key-vault-sample.md))
- Microsoft JDBC Driver versione 7.0.0 - le versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.6.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample.md))
- Microsoft JDBC Driver versione 6.4.0 - le versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.4.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Microsoft JDBC Driver versione 6.2.2 - le versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.4.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Microsoft JDBC Driver versione 6.0.0 - le versioni delle dipendenze: Azure-Keyvault (versione 0.9.7), Adal4j (versione 1.3.0) e le relative dipendenze ( [applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Con le versioni di driver 6.2.2 e 6.4.0, la dipendenza di azure-keyvault-java è stata aggiornata alla versione 1.0.0. Tuttavia, la nuova versione non è compatibile con la versione precedente (0.9.7) e si interrompe l'implementazione esistente nel driver. La nuova implementazione nel driver ha richiesto modifiche API, che a sua volta suddivide i programmi client che usano il Provider di insieme di credenziali delle chiavi di Azure.
>
> Questo problema viene risolto con versione più recente del driver (7.0.0). Il costruttore rimosso che utilizzato il meccanismo di callback di autenticazione viene nuovamente aggiunto a Azure Key Vault Provider per la compatibilità con le versioni precedenti.

### <a name="working-with-azure-active-directory-authentication"></a>Utilizzo dell'autenticazione di Azure Active Directory:

- Microsoft JDBC Driver versione 7.2.1 - le versioni delle dipendenze: Adal4j (versione 1.6.3), Client-Runtime-per-AutoRest (1.6.5) e le relative dipendenze
- Microsoft JDBC Driver versione 7.0.0 - le versioni delle dipendenze: Adal4j (versione 1.6.0) e le relative dipendenze
- Microsoft JDBC Driver versione 6.4.0 - le versioni delle dipendenze: Adal4j (versione 1.4.0) e le relative dipendenze
- Microsoft JDBC Driver versione 6.2.2 - le versioni delle dipendenze: Adal4j (versione 1.4.0) e le relative dipendenze
- Microsoft JDBC Driver versione 6.0.0 - le versioni delle dipendenze: Adal4j (versione 1.3.0) e le relative dipendenze. In questa versione del driver, è possibile connettersi tramite _ActiveDirectoryIntegrated_ modalità di autenticazione solo su un sistema operativo Windows e con sqljdbc_auth e Active Directory Authentication Library per SQL Server ( ADALSQL. DLL).

Da driver versione 6.4.0 in poi, le applicazioni non necessariamente richiedono l'uso di ADALSQL. DLL nei sistemi operativi Windows. Per la *sistemi operativi non Windows*, il driver richiede un ticket Kerberos per lavorare con l'autenticazione ActiveDirectoryIntegrated. Per altre informazioni su come connettersi ad Active Directory con Kerberos, vedere [ticket Kerberos impostato su Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Per la *sistemi operativi Windows*, il driver cercherà sqljdbc_auth per impostazione predefinita e non richiede installazione di ticket Kerberos o le dipendenze della libreria di Azure. Se sqljdbc_auth non è disponibile, il driver cercherà il ticket Kerberos per l'autenticazione ad Active Directory come altri sistemi operativi.

È possibile ottenere un [applicazione di esempio](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) che usa questa funzionalità.

## <a name="see-also"></a>Vedere anche

[Repository GitHub del Driver JDBC](https://github.com/microsoft/mssql-jdbc)  
 [Informazioni di riferimento sull'API del driver JDBC](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
