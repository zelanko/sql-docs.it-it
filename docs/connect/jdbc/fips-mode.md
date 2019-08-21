---
title: Modalità FIPS in JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028059"
---
# <a name="fips-mode"></a>Modalità FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC driver per SQL Server supporta l'esecuzione di in JVM configurato per essere conforme allo *standard FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- JVM configurato FIPS
- Certificato SSL appropriato
- File di criteri appropriati
- Parametri di configurazione appropriati

## <a name="fips-configured-jvm"></a>JVM configurato FIPS

In genere, le applicazioni possono `java.security` configurare il file per l'utilizzo di provider di crittografia conformi a FIPS. Per informazioni sulla configurazione della conformità FIPS 140, vedere la documentazione specifica per la JVM.

Per visualizzare i moduli approvati per la configurazione FIPS, fare riferimento a [moduli convalidati nel programma di convalida del modulo crittografico](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

I fornitori possono eseguire alcuni passaggi aggiuntivi per configurare una JVM con FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificato SSL appropriato
Per connettersi a SQL Server in modalità FIPS, è necessario un certificato SSL valido. Installarlo o importarlo nell'archivio chiavi Java nel computer client (JVM) in cui è abilitato FIPS.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importazione del certificato SSL nell'archivio chiavi Java
Per FIPS, è molto probabile che sia necessario importare il certificato (con estensione CERT) in PKCS o in un formato specifico del provider.
Usare il frammento di codice seguente per importare il certificato SSL e archiviarlo in una directory di lavoro con il formato di archivio chiavi appropriato. _La\_password\_dell'archivio_ di attendibilità è la password per l'archivio chiavi Java.

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

Nell'esempio seguente viene importato un certificato SSL di Azure in formato PKCS12 con il provider BouncyCastle. Il certificato viene importato nella directory di lavoro denominata _MyTrustStore\_PKCS12_ usando il frammento di codice seguente:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>File di criteri appropriati
Per alcuni provider FIPS sono necessari jar di criteri senza restrizioni. In questi casi, per Sun/Oracle, scaricare i file dei criteri di giurisdizione di JCE (Java Cryptography Extension) illimitati per [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parametri di configurazione appropriati
Per eseguire il driver JDBC in modalità conforme a FIPS, configurare le proprietà di connessione come illustrato nella tabella seguente. 

#### <a name="properties"></a>Proprietà 

|Proprietà|Tipo|Default|Descrizione|Note|
|---|---|---|---|---|
|encrypt|booleano ["true/false"]|"false"|Per la proprietà di crittografia JVM abilitata per FIPS deve essere **true**||
|TrustServerCertificate|booleano ["true/false"]|"false"|Per FIPS, l'utente deve convalidare la catena di certificati, quindi l'utente deve usare il valore **"false"** per questa proprietà. ||
|trustStore|String|null|Il percorso del file dell'archivio chiavi Java in cui è stato importato il certificato. Se si installa il certificato nel sistema, non è necessario passare alcun elemento. Il driver usa i file cacerts o jssecacerts.||
|trustStorePassword|String|null|Password utilizzata per verificare l'integrità dei dati del file trustStore.||
|fips|booleano ["true/false"]|"false"|Per la JVM abilitata per FIPS questa proprietà deve essere **true**|Aggiunto in 6.1.4 (versione stabile 6.2.2)||
|fipsProvider|String|null|Provider FIPS configurato in JVM. Ad esempio, BCFIPS o SunPKCS11-NSS |Aggiunto in 6.1.2 (versione stabile 6.2.2), deprecato in 6.4.0. vedere [qui](https://github.com/Microsoft/mssql-jdbc/pull/460)i dettagli.|
|trustStoreType|String|JKS|Per la modalità FIPS impostare il tipo di archivio attendibilità PKCS12 o tipo definito dal provider FIPS |Aggiunto in 6.1.2 (versione stabile 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
