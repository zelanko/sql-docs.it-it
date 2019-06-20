---
title: Uso di servizi desktop remoto con ODBC Connection Pooling | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14f06b98896a63f8e19ce22fb9cd1eb5b181f481
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699255"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>Uso di RDS con pool di connessioni ODBC
Se si usa un'origine dati ODBC, è possibile usare l'opzione in Internet Information Services (IIS) al pool per ottenere la gestione di ad alte prestazioni del carico di lavoro client. Pool di connessioni è un gestore di risorse per le connessioni, mantenere lo stato aperto per le connessioni utilizzate di frequente.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Per abilitare il pool di connessioni, vedere la documentazione di Internet Information Services.  
  
 Si noti che l'abilitazione del pool di connessioni può comportare il server Web da altre restrizioni, come illustrato nella documentazione di Microsoft Internet Information Services.  
  
 Per garantire che il pool di connessioni è stabile e offre ulteriori miglioramenti delle prestazioni, è necessario configurare Microsoft SQL Server per usare la libreria di rete TCP/IP Socket.  
  
 A tale scopo, è necessario:  
  
-   Configurare il computer di SQL Server per usare i socket TCP/IP.  
  
-   Configurare il server Web per usare i socket TCP/IP.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>Configurazione del Computer SQL Server per usare i socket TCP/IP  
 Nel computer SQL Server, eseguire il programma di installazione di SQL Server in modo che le interazioni con l'origine dati usano la libreria di rete TCP/IP Socket.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>Per specificare la libreria di rete del Socket TCP/IP nel computer SQL Server  
  
### <a name="in-microsoft-sql-server-65"></a>In Microsoft SQL Server 6.5:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 6.5 e quindi fare clic su installazione di SQL.  
  
2.  Fare doppio clic su Continua.  
  
3.  In Microsoft SQL Server-finestra di dialogo Opzioni, selezionare il supporto di rete di modifica e quindi fare clic su Continua.  
  
4.  Assicurarsi che sia selezionata la casella di controllo socket TCP/IP e fare clic su OK.  
  
5.  Fare clic su continua alla fine e uscire dall'installazione.  
  
### <a name="in-microsoft-sql-server-70"></a>In Microsoft SQL Server 7.0:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 7.0 e quindi fare clic su Utilità di rete del Server.  
  
2.  Nella scheda Generale della finestra di dialogo, fare clic su Aggiungi.  
  
3.  Nella finestra di dialogo Aggiungi configurazione libreria di rete, fare clic su TCP/IP.  
  
4.  Nel numero di porta delle finestre di indirizzo Proxy, immettere l'indirizzo proxy e numero di porta fornito dall'amministratore di rete.  
  
5.  Fare clic su OK per terminare e uscire dall'installazione.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>Configurazione del Server Web per usare i socket TCP/IP  
 Sono disponibili due opzioni di configurazione del server Web per usare i socket TCP/IP. Operazioni dipende dal fatto che tutte le istanze di SQL Server sono accessibili dal server Web o solo un Server SQL specifico è accessibile dal server Web.  
  
 Se tutte le istanze di SQL Server sono accessibili dal server Web, è necessario eseguire l'utilità di configurazione di SQL Server Client sul computer server Web. La procedura seguente modifica la libreria di rete predefinito per tutte le connessioni di SQL Server eseguita dal server Web IIS per usare la libreria di rete TCP/IP Sockets.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>Per configurare il server Web (tutti i server SQL)  
  
### <a name="for-microsoft-sql-server-65"></a>For Microsoft SQL Server 6.5:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 6.5 e quindi fare clic su Utilità di configurazione di SQL Client.  
  
2.  Fare clic sulla scheda Libreria di rete.  
  
3.  Nella finestra di rete predefinito, selezionare TCP/IP Sockets.  
  
4.  Fare clic su Fine per salvare le modifiche e uscire dall'utilità.  
  
### <a name="for-microsoft-sql-server-70"></a>For Microsoft SQL Server 7.0:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 7.0 e quindi fare clic su Utilità di rete del Client.  
  
2.  Fare clic sulla scheda Generale.  
  
3.  Nella casella di libreria di rete predefinito, fare clic su TCP/IP.  
  
4.  Fare clic su OK per salvare le modifiche e uscire dall'utilità.  
  
 Se una specifica di SQL Server è accessibile da un server Web, è necessario eseguire l'utilità di configurazione di SQL Server Client sul computer server Web. Per modificare la libreria di rete per una connessione di SQL Server specifica, configurare il software Client di SQL Server sul computer server Web come indicato di seguito.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>Per configurare il server Web (SQL Server specifica)  
  
### <a name="for-microsoft-sql-server-65"></a>For Microsoft SQL Server 6.5:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 6.5 e quindi fare clic su Utilità di configurazione di SQL Client.  
  
2.  Fare clic sulla scheda Avanzate.  
  
3.  Nella finestra di Server, digitare il nome del server a cui connettersi tramite TCP/IP Sockets.  
  
4.  Nella casella nome della DLL, selezionare TCP/IP Sockets.  
  
5.  Fare clic su Aggiungi/modifica. Tutte le origini dati che punta a questo server useranno i socket TCP/IP.  
  
6.  Fare clic su Fine.  
  
### <a name="for-microsoft-sql-server-70"></a>For Microsoft SQL Server 7.0:  
  
1.  Dal menu Start, scegliere Programmi Microsoft SQL Server 7.0 e quindi fare clic su Utilità di configurazione del Client.  
  
2.  Fare clic sulla scheda Generale.  
  
3.  Fare clic su Aggiungi.  
  
4.  Nella finestra di alias Server, immettere l'alias del server. Nella casella di librerie di rete, fare clic su TCP/IP. Nella casella Nome Computer, immettere il nome del computer del computer in cui è in ascolto per i client TCP/IP Sockets. Nella casella Numero porta, immettere la porta su cui è in ascolto di SQL Server.  
  
5.  Fare clic su OK e quindi di nuovo OK per uscire dall'utilità.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali su RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















