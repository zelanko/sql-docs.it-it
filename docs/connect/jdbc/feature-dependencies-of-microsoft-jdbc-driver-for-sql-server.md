---
title: Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 939a8773-2583-49a4-bf00-6b892fbe39dc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abf0d389217535292260b6a5b055697eb4b19df
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028088"
---
# <a name="feature-dependencies-of-the-microsoft-jdbc-driver-for-sql-server"></a>Dipendenze delle funzionalità di Microsoft JDBC Driver per SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questo articolo elenca le librerie da cui dipende Microsoft JDBC Driver per SQL Server. Il progetto contiene le dipendenze seguenti.

## <a name="compile-time"></a>Fase di compilazione

 - `com.microsoft.azure:azure-keyvault` : provider Azure Key Vault per la funzionalità Azure Key Vault Always Encrypted (facoltativo)
 - `com.microsoft.azure:adal4j` : Azure Active Directory Library per Java per la funzionalità di autenticazione di Azure Active Directory e la funzionalità Azure Key Vault (facoltativo)
 - `com.microsoft.rest:client-runtime` : Azure Active Directory Library per Java per la funzionalità di autenticazione di Azure Active Directory e la funzionalità Azure Key Vault (facoltativo)
 - `org.antlr:antlr4-runtime`: ANTLR 4 Runtime per la funzionalità useFmtOnly (facoltativo)
 - `org.osgi:org.osgi.core`: libreria OSGi Core per il supporto OSGi Framework.
 - `org.osgi:org.osgi.compendium`: libreria OSGi Compendium per il supporto OSGi Framework.

## <a name="test-time"></a>Fase di timeout

I progetti specifici che richiedono una delle funzionalità elencate precedentemente devono dichiarare in modo esplicito le rispettive dipendenze nel relativo file POM.

**Ad esempio:** quando si usa la funzionalità di autenticazione di Azure Active Directory, è necessario dichiarare di nuovo la dipendenza `adal4j` nel file POM del progetto. Vedere il frammento seguente:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>
```

**Ad esempio:** quando si usa la funzionalità Azure Key Vault, è necessario dichiarare di nuovo la dipendenza `azure-keyvault` e la dipendenza `adal4j` nel file POM del progetto. Vedere il frammento seguente:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
    <scope>compile</scope>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.6.4</version>
</dependency>

<dependency>
    <groupId>com.microsoft.rest</groupId>
    <artifactId>client-runtime</artifactId>
    <version>1.6.10</version>
</dependency>

<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="dependency-requirements-for-the-jdbc-driver"></a>Requisiti di dipendenza per il driver JDBC

### <a name="working-with-the-azure-key-vault-provider"></a>Uso del provider Azure Key Vault:

- Versione del driver JDBC 7.4.1 - Versioni delle dipendenze: Azure-Keyvault (versione 1.2.1), Adal4j (versione 1.6.4), Client-Runtime-for-AutoRest (1.6.10) e relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versione del driver JDBC 7.2.2 - Versioni delle dipendenze: Azure-Keyvault (versione 1.2.0), Azure-Keyvault-Webkey (versione 1.2.0), Adal4j (versione 1.6.3), Client-Runtime-for-AutoRest (1.6.5) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versione del driver JDBC 7.0.0 - Versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.6.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-7.0.md))
- Versione del driver JDBC 6.4.0 - Versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.4.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versione del driver JDBC 6.2.2 - Versioni delle dipendenze: Azure-Keyvault (versione 1.0.0), Adal4j (versione 1.4.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.2.2.md))
- Versione del driver JDBC 6.0.0 - Versioni delle dipendenze: Azure-Keyvault (versione 0.9.7), Adal4j (versione 1.3.0) e le relative dipendenze ([applicazione di esempio](../../connect/jdbc/azure-key-vault-sample-version-6.0.0.md))

> [!NOTE]
> Con le versioni del driver 6.2.2 e 6.4.0, la dipendenza azure-keyvault-java era stata aggiornata alla versione 1.0.0. La nuova versione non era tuttavia compatibile con la versione precedente (0.9.7) e interrompe l'implementazione esistente nel driver. La nuova implementazione nel driver ha richiesto modifiche API, che a loro volta interrompono i programmi client che usano il provider Azure Key Vault.
>
> Questo problema viene risolto con le versioni più recenti del driver (dalla 7.0.0 in poi). Il costruttore rimosso che usava il meccanismo di callback dell'autenticazione è stato nuovamente aggiunto al provider Azure Key Vault per la compatibilità con le versioni precedenti.

### <a name="working-with-azure-active-directory-authentication"></a>Uso dell'autenticazione di Azure Active Directory:

- Versione del driver JDBC 7.4.1 - Versioni delle dipendenze: Adal4j (versione 1.6.4), Client-Runtime-for-AutoRest (1.6.10) e le relative dipendenze
- Versione del driver JDBC 7.2.2 - Versioni delle dipendenze: Adal4j (versione 1.6.3), Client-Runtime-for-AutoRest (1.6.5) e le relative dipendenze
- Versione del driver JDBC 7.0.0 - Versioni delle dipendenze: Adal4j (versione 1.6.0) e le relative dipendenze
- Versione del driver JDBC 6.4.0 - Versioni delle dipendenze: Adal4j (versione 1.4.0) e le relative dipendenze
- Versione del driver JDBC 6.2.2 - Versioni delle dipendenze: Adal4j (versione 1.4.0) e le relative dipendenze
- Versione del driver JDBC 6.0.0 - Versioni delle dipendenze: Adal4j (versione 1.3.0) e le relative dipendenze. In questa versione del driver è possibile connettersi tramite la modalità di autenticazione _ActiveDirectoryIntegrated_ solo in un sistema operativo Windows e usando sqljdbc_auth e Active Directory Authentication Library per SQL Server (ADALSQL. DLL).

A partire dalla versione 6.4.0 del driver, le applicazioni non richiedono necessariamente l'uso di ADALSQL.DLL nei sistemi operativi Windows. Per i *sistemi operativi non Windows*, il driver richiede un ticket Kerberos per l'uso dell'autenticazione ActiveDirectoryIntegrated. Per altre informazioni su come connettersi ad Active Directory con Kerberos, vedere [Impostare i ticket Kerberos in Windows, Linux e Mac](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac).

Per i *sistemi operativi Windows*, il driver cerca sqljdbc_auth.dll per impostazione predefinita e non richiede né l'impostazione di un ticket Kerberos né le dipendenze libreria Azure. Se sqljdbc_auth.dll non è disponibile, il driver cerca il ticket Kerberos per l'autenticazione in Active Directory, come accade per gli altri sistemi operativi.

È possibile ottenere un'[applicazione di esempio](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md) che usa questa funzionalità.

## <a name="see-also"></a>Vedere anche

[Repository GitHub del driver JDBC](https://github.com/microsoft/mssql-jdbc)  
[Informazioni di riferimento sull'API del driver JDBC](../../connect/jdbc/reference/jdbc-driver-api-reference.md)
