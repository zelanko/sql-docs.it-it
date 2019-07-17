---
title: Rimozione di SSMA per DB2 componenti (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 25c8222009c2ea9358c0bab2ad5ae077588fb3cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060087"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Rimozione di SSMA per DB2 componenti (DB2ToSQL)
Dopo aver finito di migrazione di database da DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si potrebbe voler disinstallare i componenti SSMA. È possibile disinstallare i componenti client in qualsiasi momento. Tuttavia, non è necessario disinstallare il pacchetto di estensione dalla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a meno che i database migrati non usano più funzioni nel **ssma_DB2** dello schema del **sysdb** database.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Disinstallazione di SSMA per DB2 Client  
È possibile disinstallarlo con SSMA **Aggiungi / Rimuovi programmi**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.  
  
2.  Selezionare  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per DB2**, quindi fare clic su **Rimuovi**.  
  
3.  Per confermare che si desidera disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallare il pacchetto di estensione  
Se si è certi dei database migrati non usano gli oggetti di **sysdb.ssma_DB2** dello schema, è possibile rimuovere il pacchetto di estensione eliminandola dallo schema: è disponibile alcuna disinstallazione di Windows  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Installazione di componenti SSMA in SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
