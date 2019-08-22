---
title: Utilizzo dell'autenticazione NTLM per la connessione a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 2fab4794544ada07e0bf5e690da35b72ad6b7421
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026097"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>Utilizzo dell'autenticazione NTLM per la connessione a SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Consente a un'applicazione di utilizzare la proprietà di connessione **authenticationScheme** per indicare che desidera connettersi a un database utilizzando l'autenticazione NTLM v2. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 

Per l'autenticazione NTLM vengono utilizzate anche le proprietà seguenti:

- **dominio = DomainName** opzionale
- **utente = nome utente**
- **password = password**
- **integratedSecurity = true**

Ad eccezione del **dominio**, le altre proprietà sono obbligatorie, il driver genererà un errore se mancante quando viene usata la proprietà authenticationScheme **NTLM** . 

Per ulteriori informazioni sulle proprietà di connessione, vedere [impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md). Per ulteriori informazioni sul protocollo Microsoft NTLM Authentication, vedere [Microsoft NTLM](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm).

## <a name="remarks"></a>Remarks

Vedere [sicurezza di rete: livello di autenticazione di LAN Manager](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) per la descrizione delle impostazioni di SQL Server, che controllano il comportamento dell'autenticazione NTLM. 

## <a name="logging"></a>Registrazione

È stato aggiunto un nuovo logger per supportare l'autenticazione NTLM: com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication. Per altre informazioni, vedere [Creazione di tracce](../../connect/jdbc/tracing-driver-operation.md).

## <a name="datasource"></a>DataSource

Quando si utilizza un'origine dati per creare connessioni, le proprietà NTLM possono essere impostate a livello di codice utilizzando **setAuthenticationScheme**, **sedomain** e (facoltativamente) **setServerSpn**.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>Nomi dell'entità servizio

Un nome dell'entità servizio (SPN) è il nome con cui un client identifica in modo univoco un'istanza di un servizio.

È possibile specificare il nome dell'entità servizio usando la proprietà di connessione **serverSpn** o lasciare che sia il driver a crearlo automaticamente (impostazione predefinita). Questa proprietà usa il formato: "MSSQLSvc/fqdn:porta\@AREADIAUTENTICAZIONE", dove fqdn è il nome di dominio completo, porta è il numero di porta e AREADIAUTENTICAZIONE è l'area di autenticazione di SQL Server in lettere maiuscole. La parte area di autenticazione di questa proprietà è facoltativa perché l'area di autenticazione predefinita è la stessa dell'area di autenticazione del server.

Il nome SPN, ad esempio, potrebbe essere simile al seguente: "MSSQLSvc/some-server. zzz. Corp. contoso. com: 1433"

Per ulteriori informazioni sui nomi dell'entità servizio (SPN), vedere:

- [Supporto del nome dell'entità servizio (SPN) nelle connessioni client](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> L'attributo di connessione serverSpn è supportato solo da Microsoft JDBC Driver 4.2 e versioni successive.

> Prima della versione 6,2 del driver JDBC, è necessario impostare in modo esplicito **serverSpn**. A partire dalla versione 6,2, il driver sarà in grado di compilare **serverSpn** per impostazione predefinita, anche se è possibile usare **serverSpn** in modo esplicito.

## <a name="security-risks"></a>Rischi per la sicurezza

Il protocollo NTLM è un protocollo di autenticazione obsoleto con diverse vulnerabilità, che rappresentano un rischio per la sicurezza. Si basa su uno schema crittografico relativamente debole ed è vulnerabile a diversi attacchi. Viene sostituito con Kerberos, che è molto più sicuro e consigliato. L'autenticazione NTLM deve essere utilizzata solo in un ambiente attendibile sicuro oppure quando non è possibile utilizzare Kerberos.

Supporta [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] solo NTLM v2, che offre alcuni miglioramenti per la sicurezza rispetto al protocollo v1 originale. It'ss consiglia inoltre di abilitare la protezione estesa o di utilizzare la crittografia SSL per una maggiore sicurezza. 

Per ulteriori informazioni su come abilitare la protezione estesa e, vedere:

- [Connessione al motore di database mediante la protezione estesa](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

Per ulteriori informazioni sulla connessione con la crittografia SSL, vedere:

- [Connessione tramite la crittografia SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> Per la versione 7,4, l' **abilitazione** della protezione estesa e della crittografia non è supportata.

## <a name="see-also"></a>Vedere anche

[Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
