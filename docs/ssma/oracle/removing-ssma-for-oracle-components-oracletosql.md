---
title: Rimozione di SSMA per componenti Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0434f88c46d14672c84f5f7939488a827b229e27
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266556"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Rimozione di SSMA per i componenti Oracle (OracleToSQL)
Dopo aver finito di migrazione di database da Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si potrebbe voler disinstallare i componenti SSMA. È possibile disinstallare i componenti client in qualsiasi momento. Tuttavia, non è necessario disinstallare il pacchetto di estensione dalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a meno che i database migrati non usano più funzioni nel **ssma_oracle** dello schema del **sysdb** database.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Disinstallazione di SSMA per Oracle Client  
È possibile disinstallarlo con SSMA **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Oracle**, quindi fare clic su **Rimuovi**.  
  
3.  Per confermare che si desidera disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallare il pacchetto di estensione  
Se si è certi dei database migrati non usano gli oggetti di **sysdb.ssma_oracle** dello schema, è possibile rimuovere il pacchetto di estensione usando **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare il pacchetto di estensione**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare **Microsoft SQL Server Migration Assistant per Oracle Extension Pack**, quindi fare clic su **rimuovere**.  
  
3.  Per confermare che si desidera disinstallare il pacchetto di estensione, fare clic su **Sì**.  
  
4.  Nelle istanze con pagina di script dell'utilità del Database, selezionare un'istanza e quindi fare clic su **successivo**.  
  
5.  Nella pagina parametri per la connessione, selezionare il metodo di autenticazione e quindi fare clic su **successivo**.  
  
    L'autenticazione di Windows userà le credenziali di Windows per tentare di accedere all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si seleziona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione, è necessario immettere un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome account di accesso e la password.  
  
6.  Nella pagina operazione completata, fare clic su **OK**.  
  
7.  Nell'ultima pagina, fare clic su **Exit**.  
  
Dopo la disinstallazione, è possibile verificare che gli oggetti nel **sysdb.ssma_oracle** schema ed eventualmente l'intera **sysdb** del database, è stato rimosso usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Tuttavia, se si utilizzano altri prodotti SSMA, sono anche usare il **sysdb** database. Se il database esista e si è certi che nessun altro database fanno riferimento a oggetti in questo database, è possibile scollegare il database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Installazione di componenti SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
