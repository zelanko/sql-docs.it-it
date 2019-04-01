---
title: Modalità FIPS in JDBC | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 8fb6ea7bf6abfb1f347d0541a01bae91aacf5f1c
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618278"
---
# <a name="fips-mode"></a>Modalità FIPS
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver per SQL Server supporta l'esecuzione nella JVM configurato per essere *compatibili con FIPS 140*.

#### <a name="prerequisites"></a>Prerequisites

- FIPS configurato JVM
- Certificato SSL appropriato
- File dei criteri appropriati
- Parametri di configurazione appropriato

## <a name="fips-configured-jvm"></a>FIPS configurato JVM

In generale, è possono configurare le applicazioni di `java.security` file da usare provider di crittografia compatibili con FIPS. Vedere la documentazione specifica per JVM per informazioni su come configurare la conformità FIPS 140.

Per visualizzare i moduli approvati per la configurazione di FIPS, vedere [convalidati i moduli del programma di convalida crittografia modulo](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules).

I fornitori possono avere alcuni passaggi aggiuntivi per configurare una JVM a FIPS.

## <a name="appropriate-ssl-certificate"></a>Certificato SSL appropriato
Per connettersi a SQL Server in modalità FIPS, è necessario un certificato SSL valido. Installare o importarla Java Key Store nel computer client (JVM) in cui è abilitato FIPS.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importare il certificato SSL nell'archivio chiavi Java
Per FIPS, molto probabilmente è necessario importare il certificato (con estensione CERT) in un formato specifico del provider o PKCS.
Usare il frammento di codice seguente per importare il certificato SSL e archiviarlo in una directory di lavoro con il formato dell'archivio chiavi appropriata. _TRUST\_STORE\_PASSWORD_ è la password per archivio chiavi Java.

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

Nell'esempio seguente importa un certificato SSL di Azure nel formato PKCS12 con il BouncyCastle Provider. Il certificato viene importato nella directory di lavoro denominata _MyTrustStore\_PKCS12_ usando il frammento seguente:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>File dei criteri appropriati
Per alcuni provider di FIPS, sono necessari file JAR di criteri senza restrizioni. In questi casi, per Sun / Oracle, scaricare il Java Cryptography Extension (JCE) senza limiti Strenght Jurisdiction Policy Files per [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) oppure [JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parametri di configurazione appropriato
Per eseguire il Driver JDBC in modalità FIPS compatibile, configurare le proprietà di connessione come illustrato nella tabella seguente. 

#### <a name="properties"></a>Proprietà 

|Proprietà|Tipo|Default|Descrizione|Note|
|---|---|---|---|---|
|encrypt|booleano ["true/false"]|"false"|Per FIPS abilitata JVM crittografa la proprietà deve essere **true**||
|TrustServerCertificate|booleano ["true/false"]|"false"|Per FIPS, l'utente deve convalidare la catena di certificati in modo che l'utente deve usare **"false"** valore per questa proprietà. ||
|trustStore|String|null|Il percorso del file dell'archivio chiavi Java in cui è stato importato il certificato. Se si installa certificato nel sistema, quindi non è necessario passare un valore. Driver utilizza file cacerts o jssecacerts.||
|trustStorePassword|String|null|Password utilizzata per verificare l'integrità dei dati del file trustStore.||
|fips|booleano ["true/false"]|"false"|Per JVM abilitato FIPS questa proprietà deve essere **true**|Aggiunto in 6.1.4 (stabile versione 6.2.2)||
|fipsProvider|String|null|Provider FIPS configurato nella JVM. Ad esempio, BCFIPS o SunPKCS11 NSS |Aggiunto in 6.1.2 (stabile versione 6.2.2), deprecato in 6.4.0 - visualizzare i dettagli [qui](https://github.com/Microsoft/mssql-jdbc/pull/460).|
|trustStoreType|String|JKS|Per tipo di archivio trust set modalità FIPS PKCS12 o tipo definito dal provider FIPS |Aggiunto in 6.1.2 (stabile versione 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
