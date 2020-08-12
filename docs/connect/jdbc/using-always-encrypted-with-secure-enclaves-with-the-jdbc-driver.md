---
title: Uso di Always Encrypted con enclave sicuri con JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: reneye
ms.author: v-reye
ms.openlocfilehash: 8933d01f8c1bb0e028927b1c0f97f064a369bb8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758282"
---
# <a name="using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver"></a>Uso di Always Encrypted con enclave sicuri con JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Questa pagina include informazioni su come sviluppare applicazioni Java usando [Always Encrypted con enclave sicure](../../relational-databases/security/encryption/always-encrypted-enclaves.md) e Microsoft JDBC Driver 8.2 (o versioni successive) per SQL Server.

Le enclavi sicure sono un'aggiunta alla funzionalità [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) esistente. Lo scopo delle enclavi sicure è gestire le limitazioni quando si lavora con dati Always Encrypted. In precedenza, gli utenti potevano solo eseguire confronti di uguaglianza sui dati Always Encrypted e dovevano recuperare e decrittografare i dati per eseguire altre operazioni. Le enclavi sicure consentono di superare queste limitazioni, permettendo l'esecuzione di calcoli su dati di testo non crittografato all'interno di un enclave sicura sul lato server. Un enclave sicuro è un'area protetta della memoria all'interno del processo di SQL Server e agisce come un ambiente di esecuzione affidabile per l'elaborazione dei dati sensibili all'interno del motore di SQL Server. Un enclave sicuro viene visualizzato come black box per il resto di SQL Server e altri processi nel computer host. Non vi è alcun modo per visualizzare dati o codice all'interno dell'enclave dall'esterno, anche con un debugger.

## <a name="prerequisites"></a>Prerequisiti
- Assicurarsi che nel computer di sviluppo sia installato Microsoft JDBC Driver 8.2 (o versione successiva) per SQL Server.
- Verificare che le dipendenze dell'ambiente, ad esempio DLL, archivi di chiavi e così via, si trovino nei percorsi corretti. Always Encrypted con enclave sicuri è un componente aggiuntivo della funzionalità [Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md) esistente ed entrambi condividono prerequisiti simili.

> [!Note]
> Se si usa una versione precedente di JDK 8, potrebbe essere necessario scaricare e installare i file di criteri di giurisdizione di forza illimitata JCE (Java Cryptography Extension). Leggere il file leggimi incluso nel file ZIP per istruzioni sull'installazione e dettagli rilevanti sui possibili problemi di importazione/esportazione.  
>
> I file dei criteri possono essere scaricati da [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

## <a name="setting-up-secure-enclaves"></a>Configurazione di enclave sicure
Seguire questa [esercitazione](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md) per informazioni introduttive sull'uso delle enclavi sicure. Per informazioni più dettagliate, vedere [Always Encrypted con enclave sicure](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="connection-string-properties"></a>Proprietà per la stringa di connessione
**enclaveAttestationUrl:** URL dell'endpoint del servizio di attestazione.

**enclaveAttestationProtocol:** protocollo del servizio di attestazione. Attualmente, l'unico valore supportato è **HGS**(servizio Sorveglianza host).

Gli utenti devono abilitare **columnEncryptionSetting** e impostare correttamente **entrambe** le proprietà della stringa di connessione sopra indicate per abilitare Always Encrypted con enclave sicure da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

## <a name="working-with-secure-enclaves"></a>Uso delle enclavi sicure
Quando le proprietà di connessione dell'enclave sono impostate correttamente, il funzionamento è trasparente. Il driver determina se la query richiede l'uso automatico di un'enclave sicura. Di seguito sono riportati alcuni esempi di query che attivano i calcoli dell'enclave. Per informazioni sulla configurazione di database e tabelle, vedere [Introduzione alle enclave Always Encrypted](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md).

Le query complesse attiveranno i calcoli dell'enclave:
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL)) {
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SSN LIKE ?")) {
        p.setString(1, "%6818");
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
    
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SALARY > ?")) {
        ((SQLServerPreparedStatement) p).setMoney(1, new BigDecimal(0));
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
}
```

Per attivare o disattivare la crittografia in una colonna vengono attivati anche i calcoli dell'enclave:
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL);Statement s = c.createStatement()) {
    s.executeUpdate("ALTER TABLE Employees ALTER COLUMN SSN CHAR(11) NULL WITH (ONLINE = ON)");
}
```

## <a name="java-8-users"></a>Utenti di Java 8
Questa funzionalità richiede l'algoritmo di firma RSASSA-PSA. Questo algoritmo è stato aggiunto in JDK 11, ma non è stato eseguito il backporting a JDK 8. Gli utenti che desiderano usare questa funzionalità con la versione JDK 8 del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] devono caricare il proprio provider, che supporta l'algoritmo di firma RSASSA-PSA, o includere la dipendenza facoltativa BouncyCastleProvider. La dipendenza verrà rimossa in un secondo momento in caso di backporting dell'algoritmo di firma in JDK 8 o se termina il ciclo di vita del supporto di JDK 8.

## <a name="see-also"></a>Vedere anche
[Uso di Always Encrypted con il driver JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  