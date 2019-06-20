---
title: Rimozione di SSMA per componenti di MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ad23c4add9b6e7ea9999a434261a95282f129935
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182052"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Rimozione dei componenti di SSMA per MySQL (MySQLToSql)
Dopo aver finito di migrazione di database da MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si potrebbe voler disinstallare i componenti SSMA. È possibile disinstallare i componenti client in qualsiasi momento. Tuttavia, se si disinstalla il pacchetto di estensioni da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quindi, SSMA non supporteranno più della migrazione dei dati da MySQL a database di destinazione (SQL Server/SQL Azure) usando il modulo di migrazione dei dati lato Server.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Disinstallazione di SSMA per il Client MySQL  
È possibile disinstallarlo con SSMA **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per MySQL**, quindi fare clic su **rimuovere**.  
  
3.  Per confermare che si desidera disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallare il pacchetto di estensione  
È possibile rimuovere il pacchetto di estensione usando **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare il pacchetto di estensione**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per MySQL Extension Pack**, quindi fare clic su **rimuovere**.  
  
3.  Per confermare che si desidera disinstallare il pacchetto di estensione, fare clic su **Sì**.  
  
4.  Nelle istanze con pagina di script dell'utilità del Database, selezionare un'istanza e quindi fare clic su **successivo**.  
  
5.  Nella pagina parametri per la connessione, selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome account di accesso e la password.  
  
6.  Nella pagina operazione completata, fare clic su **OK**.  
  
7.  Nell'ultima pagina, fare clic su **Exit**.  
  
Dopo aver completato il processo di disinstallazione, è possibile verificare che gli oggetti nel **sysdb.ssma_MySQL** schema ed eventualmente l'intera **sysdb** del database, è stato rimosso usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, se si utilizzano altri prodotti SSMA, sono anche usare il **sysdb** database. Se il database esista e si è certi che nessun altro database fanno riferimento agli oggetti in questo database, è possibile scollegare il database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per MySQL Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Installazione di componenti SSMA in SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
