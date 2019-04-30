---
title: Installazione di componenti SSMA in SQL Server (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1f80198787dd85d8f0c65e9881925641f9f081e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233044"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Installazione dei componenti SSMA in SQL Server (MySQLToSql)
Oltre a installare SSMA, è necessario installare anche i componenti nel computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi componenti includono il pacchetto di estensioni SSMA, che supporta la migrazione dei dati e provider di MySQL per consentire la connettività server-to-server.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA per il pacchetto di estensione MySQL  
Viene aggiunto un database, il pacchetto di estensioni SSMA **sysdb**, per l'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo database contiene tabelle e stored procedure necessarie per la migrazione dei dati.  
  
Inoltre, quando si esegue la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], crea SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processi di Agent, quando il modulo di migrazione dei dati lato server viene usato per la migrazione dei dati.  
  
### <a name="prerequisites"></a>Prerequisiti  
Prima di installare SSMA per componenti di server MySQL in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assicurarsi che il computer soddisfi i requisiti seguenti:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o versione successiva.  
  
-   Il Provider Client MySQL e la connettività al database MySQL che si desidera eseguire la migrazione. È possibile installare i provider dal sito Web di MySQL o MySQL supporti del prodotto.  
  
-   Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser deve essere eseguito durante l'installazione. Viene utilizzato per popolare un elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nell'installazione guidata. È possibile disabilitare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser dopo l'installazione.  
  
    > [!NOTE]  
    > Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Browser è in esecuzione, ma ancora non è presente un elenco di istanze nel programma di installazione, è necessario sbloccare la porta UDP 1434. È possibile usare Windows Firewall per temporaneamente sbloccare la porta oppure è possibile disabilitare temporaneamente Windows Firewall. Potrebbe anche essere necessario disabilitare temporaneamente il software antivirus. Assicurarsi di abilitare i firewall e software antivirus dopo l'installazione.  
  
### <a name="installing-the-extension-pack"></a>Installare il pacchetto di estensione  
È possibile installare qualsiasi momento prima della migrazione dei dati per il pacchetto di estensione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Per installare il pacchetto di estensione, è necessario essere un membro del **sysadmin** ruolo del server nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per installare il pacchetto di estensione**  
  
1.  Copiare SSMA per MySQL Extension Pack. *n*. Install.exe, dove *n* è il numero di build, al computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Fare doppio clic su SSMA per MySQL Extension Pack. *n*. Install.exe.  
  
3.  Nella finestra di dialogo di benvenuto, fare clic su **successivo**.  
  
4.  Nella finestra di dialogo Contratto di licenza leggere il contratto di licenza. Se si accetta, selezionare la **accetto i termini del contratto di licenza** casella di controllo e quindi fare clic su **successivo**.  
  
5.  Nella finestra di dialogo Selezione tipo di installazione, fare clic su **tipica**.  
  
6.  Nella pronto per la finestra di dialogo di installazione, fare clic su **installare**.  
  
7.  Nella finestra di dialogo di installazione del primo passaggio completato, fare clic su **successivo**.  
  
    Verrà visualizzata una nuova finestra di dialogo, in cui si seleziona l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'installazione del pacchetto di estensione.  
  
8.  Selezionare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui faranno la migrazione degli schemi di MySQL e quindi fare clic **successivo**.  
  
    L'istanza predefinita ha lo stesso nome del computer. Le istanze denominate saranno seguite da una barra rovesciata e il nome dell'istanza.  
  
9. Nella finestra di dialogo di connessione, selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome account di accesso e la password.  
  
10. Nella successiva finestra di dialogo, selezionare **installare Database Utilities** *n*, dove *n* è il numero di versione e quindi fare clic su **Avanti**.  
  
    Il **sysdb** database viene creato con le tabelle e stored procedure necessarie per la migrazione dei dati (tramite modulo di migrazione dei dati lato server) vengono create in tale database.  
  
11. Per installare le utilità in un'altra istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selezionare **Yes**, quindi fare clic su **successivo**. Per uscire dalla procedura guidata, fare clic **No**.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per MySQL Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
