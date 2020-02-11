---
title: Rimozione dei componenti SSMA per MySQL (MySQLToSql) | Microsoft Docs
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
ms.openlocfilehash: 3a5d6d1234cc294cc8e8cdd163ce8a9bd6ac3e3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929381"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Rimozione dei componenti di SSMA per MySQL (MySQLToSql)
Al termine della migrazione dei database da MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], potrebbe essere necessario disinstallare i componenti di SSMA. È possibile disinstallare i componenti client in qualsiasi momento. Tuttavia, se si disinstalla il pacchetto di estensione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da, SSMA non supporterà più la migrazione dei dati da MySQL al database di destinazione (SQL Server/SQL Azure) utilizzando il motore di migrazione dei dati sul lato server.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Disinstallazione di SSMA per il client MySQL  
È possibile disinstallare SSMA utilizzando **Installazione applicazioni**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo aprire **Installazione applicazioni**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per MySQL**e quindi fare clic su **Rimuovi**.  
  
3.  Per confermare che si vuole disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallazione del pacchetto di estensione  
È possibile rimuovere il pacchetto di estensione utilizzando **Installazione applicazioni**.  
  
**Per disinstallare il pacchetto di estensione**  
  
1.  Nel Pannello di controllo aprire **Installazione applicazioni**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per MySQL Extension Pack**e quindi fare clic su **Rimuovi**.  
  
3.  Per confermare che si vuole disinstallare il pacchetto di estensione, fare clic su **Sì**.  
  
4.  Nella pagina istanze con script database utilità selezionare un'istanza e quindi fare clic su **Avanti**.  
  
5.  Nella pagina parametri connessione selezionare il metodo di autenticazione e quindi fare clic su **Avanti**.  
  
    L'autenticazione di Windows utilizzerà le credenziali di Windows per tentare di accedere all'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di, è necessario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] immettere un nome di account di accesso e una password.  
  
6.  Nella pagina operazione completata fare clic su **OK**.  
  
7.  Nella pagina fine fare clic su **Esci**.  
  
Al termine del processo di disinstallazione, è possibile verificare che gli oggetti nello schema **sysdb. ssma_MySQL** e possibilmente l'intero database **sysdb** siano stati rimossi tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, se si usano altri prodotti SSMA, viene usato anche il database **sysdb** . Se il database esiste e si è certi che nessun altro database fa riferimento agli oggetti in questo database, è possibile scollegare il database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per il client MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Installazione di componenti SSMA in SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
