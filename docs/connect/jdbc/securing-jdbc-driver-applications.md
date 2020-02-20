---
title: Protezione delle applicazioni del driver JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61a17b302499f87d552ec61c90208effc688e164
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027748"
---
# <a name="securing-jdbc-driver-applications"></a>Protezione delle applicazioni del driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Per migliorare la sicurezza di un'applicazione [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] non è sufficiente evitare i problemi comuni relativi al codice. Un'applicazione che accede ai dati presenta numerosi punti di errore potenziali che un pirata informatico può sfruttare recuperare, modificare o distruggere dati sensibili. È importante comprendere tutti gli aspetti della sicurezza, dal processo di classificazione dei rischi durante la fase di progettazione dell'applicazione all'eventuale distribuzione fino all'importanza di una continua manutenzione.  
  
Negli argomenti di questa sezione vengono descritti alcuni problemi di sicurezza comuni, inclusi quelli relativi a stringhe di connessione, convalida dell'input utente e sicurezza generale delle applicazioni.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                            | Descrizione                                                                                                                                                           |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Protezione delle stringhe di connessione](../../connect/jdbc/securing-connection-strings.md) | Vengono descritte le tecniche per la protezione delle informazioni utilizzate per la connessione a un'origine dati.                                                                                    |
| [Convalida dell'input utente](../../connect/jdbc/validating-user-input.md)             | Vengono descritte le tecniche per la convalida dell'input utente.                                                                                                                          |
| [Sicurezza dell'applicazione](../../connect/jdbc/application-security.md)               | Viene descritto come utilizzare le autorizzazioni relative ai criteri Java per proteggere un'applicazione del driver JDBC.                                                                                |
| [Uso della crittografia SSL](../../connect/jdbc/using-ssl-encryption.md)               | Viene descritto come stabilire un canale di comunicazione sicuro con un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando SSL (Secure Sockets Layer). |
| [Modalità FIPS](../../connect/jdbc/fips-mode.md)                                     | Viene descritto come usare il driver JDBC in modalità conforme a FIPS.                                                                                                              |
  
## <a name="see-also"></a>Vedere anche  

 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
