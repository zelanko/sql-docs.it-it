---
title: Protezione delle applicazioni JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3a7a8079f60336bbdfe7b837afa2313f5fda2691
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797841"
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
| [Modalità FIPS](../../connect/jdbc/fips-mode.md)                                     | Viene descritto come usare JDBC driver in modalità conforme a FIPS.                                                                                                              |
  
## <a name="see-also"></a>Vedere anche  

 [Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
