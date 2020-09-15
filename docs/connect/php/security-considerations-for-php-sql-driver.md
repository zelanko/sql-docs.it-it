---
description: Considerazioni sulla sicurezza per i driver Microsoft per PHP per SQL Server
title: Considerazioni sulla sicurezza per i driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36c5826b81c68229c5c5bffba7f19d17187447a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414387"
---
# <a name="security-considerations-for-the-microsoft-drivers-for-php-for-sql-server"></a>Considerazioni sulla sicurezza per i driver Microsoft per PHP per SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questo argomento vengono descritte considerazioni sulla sicurezza specifiche per lo sviluppo, la distribuzione e l'esecuzione di applicazioni che usano [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Per informazioni più dettagliate sulla sicurezza di SQL Server, vedere [Cenni preliminari sulla sicurezza in SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/overview-of-sql-server-security).  
  
## <a name="connect-using-windows-authentication"></a>Connettersi con l'autenticazione di Windows  
L'autenticazione di Windows deve essere usata per connettersi a SQL Server ogni volta che è possibile per i motivi seguenti:  
  
-   **Durante l'autenticazione le credenziali non vengono trasmesse attraverso la rete.** Nomi utente e password non sono incorporati nella stringa di connessione al database. Di conseguenza, utenti non autorizzati o malintenzionati non possono ottenere le credenziali monitorando la rete o visualizzando le stringhe di connessione nei file di configurazione.  
  
-   **Gli utenti sono soggetti a una gestione centralizzata degli account.** Vengono applicati criteri di sicurezza, ad esempio i periodi di scadenza delle password, la lunghezza minima delle password e il blocco degli account dopo più richieste di accesso non valide.  
  
Per informazioni su come connettersi a un server con l'autenticazione di Windows, vedere [Procedura: Connessione con l'autenticazione di Windows](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Quando ci si connette tramite l'autenticazione di Windows, è consigliabile configurare l'ambiente in modo che SQL Server possa usare il protocollo di autenticazione Kerberos. Per altre informazioni, vedere [Come assicurarsi che si utilizza l'autenticazione Kerberos quando si crea una connessione remota a un'istanza di SQL Server 2005](https://support.microsoft.com/en-ca/help/909801/how-to-make-sure-that-you-are-using-kerberos-authentication-when-you-c) o [Autenticazione Kerberos e SQL Server](https://msdn.microsoft.com/library/cc280744.aspx).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Usare connessioni crittografate durante il trasferimento di dati sensibili  
È necessario usare connessioni crittografate ogni volta che si inviano o si recuperano dati sensibili da SQL Server. Per informazioni su come abilitare connessioni crittografate, vedere [Abilitazione di connessioni crittografate al Motore di database (Gestione configurazione SQL Server)](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Per stabilire una connessione protetta con [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], usare l'attributo di connessione Encrypt durante la connessione al server. Per altre informazioni sugli attributi di connessione, vedere [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Usare query con parametri  
Per ridurre il rischio di attacchi intrusivi nel codice SQL, usare query con parametri. Per esempi di esecuzione di query con parametri, vedere [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Per altre informazioni sugli attacchi intrusivi nel codice SQL e considerazioni di sicurezza correlate, vedere [Attacco intrusivo nel codice SQL](https://msdn.microsoft.com/library/ms161953.aspx).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>Non accettare informazioni relative a server o stringhe di connessione da utenti finali  
Il codice dell'applicazione deve evitare che gli utenti finali possano inviare informazioni relative a server o stringhe di connessione all'applicazione stessa. Mantenendo uno stretto controllo sulle informazioni relative a server o a stringhe di connessione si riduce l'esposizione agli attacchi di attività dannose.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Attivare WarningsAsErrors durante lo sviluppo di applicazioni  
Sviluppare applicazioni con l'impostazione **WarningsAsErrors** su **true** in modo che gli avvisi generati dal driver vengano considerati errori. Ciò consente allo sviluppatore di risolvere gli avvisi prima di distribuire l'applicazione. Per altre informazioni, vedere [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Proteggere i log delle applicazioni distribuite  
Per le applicazioni distribuite, assicurarsi che i log vengano scritti in un percorso protetto o che la registrazione sia disabilitata. Ciò consente di evitare la possibilità che utenti finali accedano alle informazioni scritte nei file di log. Per altre informazioni, vedere [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Vedere anche  
[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
