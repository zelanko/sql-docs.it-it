---
title: Modalità FIPS in JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83ce3690d194b8b06fc79d58c2d7bc7efa996619
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293381"
---
# <a name="fips-mode"></a>Modalità FIPS

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver per SQL Server supporta l'esecuzione in JVM (Java Virtual Machine) configurate per essere *conformi a FIPS 140*.

#### <a name="prerequisites"></a>Prerequisiti

- JVM configurata per FIPS
- Certificato TLS/SSL appropriato
- File di criteri appropriati
- Parametri di configurazione appropriati

## <a name="fips-configured-jvm"></a>JVM configurata per FIPS

Le applicazioni possono in genere configurare il file `java.security` per l'uso di provider di crittografia conformi a FIPS. Per informazioni sulla configurazione della conformità FIPS 140, vedere la documentazione specifica della JVM.

Per informazioni sui moduli approvati per la configurazione FIPS, vedere [Moduli convalidati nel Programma di convalida moduli di crittografia](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

I fornitori possono prevedere passaggi aggiuntivi per configurare una JVM con FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificato SSL appropriato
Per connettersi a SQL Server in modalità FIPS, è necessario un certificato TLS/SSL valido. Installarlo o importarlo nell'archivio chiavi Java nel computer client (JVM) in cui è abilitato FIPS.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importazione del certificato SSL nell'archivio chiavi Java
Per FIPS, è molto probabile che sia necessario importare il certificato (con estensione cert) in formato PKCS o in un formato specifico del provider.
Usare il frammento di codice seguente per importare il certificato TLS/SSL e archiviarlo in una directory di lavoro con il formato di archivio chiavi appropriato. _TRUST\_STORE\_PASSWORD_ è la password per l'archivio chiavi Java.

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

Nell'esempio seguente viene importato un certificato TLS/SSL di Azure in formato PKCS12 con il provider BouncyCastle. Il certificato viene importato nella directory di lavoro denominata _MyTrustStore\_PKCS12_ usando il frammento di codice seguente:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>File di criteri appropriati
Per alcuni provider FIPS sono necessari JAR di criteri senza restrizioni. In questi casi, per Sun/Oracle, scaricare Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files per [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) o [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parametri di configurazione appropriati
Per eseguire JDBC Driver in modalità conforme a FIPS, configurare le proprietà di connessione come indicato nella tabella riportata di seguito. 

#### <a name="properties"></a>Proprietà 

|Proprietà|Type|Predefinito|Descrizione|Note|
|---|---|---|---|---|
|encrypt|booleano ["true/false"]|"false"|Per la JVM abilitata per FIPS, la proprietà encrypt deve essere **true**||
|TrustServerCertificate|booleano ["true/false"]|"false"|Per FIPS, l'utente deve convalidare la catena di certificati. Pertanto l'utente deve usare il valore **"false"** per questa proprietà. ||
|trustStore|string|Null|Il percorso del file dell'archivio chiavi Java in cui è stato importato il certificato. Se il certificato viene installato nel sistema, non è necessario passare alcun elemento. Il driver usa i file cacerts o jssecacerts.||
|trustStorePassword|string|Null|Password utilizzata per verificare l'integrità dei dati del file trustStore.||
|fips|booleano ["true/false"]|"false"|Per la JVM abilitata per FIPS, questa proprietà deve essere **true**.|Aggiunta nella versione 6.1.4 (versione stabile 6.2.2)||
|fipsProvider|string|Null|Provider FIPS configurato nella JVM. Ad esempio, BCFIPS o SunPKCS11-NSS |Aggiunta nella versione 6.1.2 (versione stabile 6.2.2), deprecata nella versione 6.4.0. Vedere i dettagli [qui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|string|JKS|Per la modalità FIPS impostare il tipo di archivio attendibilità su PKCS12 o sul tipo definito dal provider FIPS |Aggiunta nella versione 6.1.2 (versione stabile 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
