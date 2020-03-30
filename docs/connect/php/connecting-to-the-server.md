---
title: Connessione a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 789fec0bd9299f4d436c664306d380bb9a7da153
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015140"
---
# <a name="connecting-to-the-server"></a>Connessione al server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Negli argomenti di questa sezione vengono descritte le opzioni e le procedure per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

I [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] possono connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando l'autenticazione di Windows o l'autenticazione di SQL Server. Per impostazione predefinita, i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tentano di connettersi al server usando l'autenticazione di Windows.  

## <a name="in-this-section"></a>Contenuto della sezione  

|Argomento|Descrizione|  
|---------|---------------|  
|[Procedura: Connessione con l'autenticazione di Windows](../../connect/php/how-to-connect-using-windows-authentication.md)|Descrive come stabilire una connessione usando l'autenticazione di Windows.|  
|[Procedura: Connessione con l'autenticazione di SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)|Descrive come stabilire una connessione usando l'autenticazione di SQL Server.|  
|[Procedura: Connessione con l'autenticazione di Azure Active Directory](../../connect/php/azure-active-directory.md)|Illustra come impostare la modalità di autenticazione e come connettersi usando le identità di Azure Active Directory.|  
|[Procedura: Connessione a una porta specifica](../../connect/php/how-to-connect-on-a-specified-port.md)|Descrive come connettersi al server su una porta specifica.|  
|[Pool di connessioni](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|Fornisce informazioni sui pool di connessioni nel driver.|  
|[Procedura: Disabilitare più set di risultati attivi (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|Descrive come disabilitare la funzionalità MARS (Multiple Active Resultsets) quando si stabilisce una connessione.|  
|[Opzioni di connessione](../../connect/php/connection-options.md)|Elenca le opzioni che sono consentite nella matrice associativa contenente gli attributi di connessione.|  
|[Supporto per LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|Descrive il supporto dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] per la funzionalità Local DB aggiunta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Supporto per il ripristino di emergenza a disponibilità elevata](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|Illustra come configurare l'applicazione per sfruttare le funzionalità di ripristino di emergenza a disponibilità elevata aggiunte in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Connessione al database SQL di Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Tratta come connettersi a un database SQL di Azure.|  
|[Resilienza connessione](../../connect/php/connection-resiliency.md)|Illustra la funzionalità di resilienza della connessione che ristabilisce le connessioni interrotte.|  

## <a name="see-also"></a>Vedere anche  
[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Applicazione di esempio &#40;Driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
