---
title: Rimozione di SSMA per componenti di Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b3cebc9bb82778390716212fd3b5ae1bf800d3d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667933"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Rimozione di SSMA per componenti di Sybase (SybaseToSQL)
Dopo aver finito di migrazione dei database di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si potrebbe voler disinstallare i componenti SSMA. È possibile disinstallare i componenti client in qualsiasi momento, ma non è necessario disinstallare il pacchetto di estensione dalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a meno che non si è certi che i database migrati non usano più funzioni nel **ssma_syb** dello schema del **sysdb** database.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Disinstallazione di SSMA per Sybase Client  
È possibile disinstallarlo con SSMA **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per Sybase**, quindi fare clic su **rimuovere**.  
  
3.  Per confermare che si desidera disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallare il pacchetto di estensione  
Se si è certi dei database migrati non usano gli oggetti di **sysdb.ssma_syb** dello schema, è possibile rimuovere il pacchetto di estensione usando **Aggiungi / Rimuovi programmi**.  
  
Per disinstallare il pacchetto di estensione  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per Sybase Extension Pack**, quindi fare clic su **rimuovere**.  
  
3.  Per confermare che si desidera disinstallare il pacchetto di estensione, fare clic su **Sì**.  
  
4.  Nelle istanze con pagina di script dell'utilità del Database, fare clic su **successivo**.  
  
5.  Nella pagina parametri per la connessione, selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di SQL Server. Se si seleziona autenticazione di SQL Server, è necessario immettere un nome di account di accesso di SQL Server e una password.  
  
6.  Nella pagina operazione completata, fare clic su **OK**.  
  
7.  Nell'ultima pagina, fare clic su **Exit**.  
  
Dopo aver disinstallato, è possibile verificare che il **sysdb.ssma_syb** schema ed eventualmente l'intera **sysdb** del database, è stato rimosso usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, se si utilizzano altri prodotti SSMA, sono anche usare il **sysdb** database. Se il database esista e si è certi che nessun altro database fanno riferimento a oggetti in questo database, è possibile scollegare il database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Installazione di componenti SSMA in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
