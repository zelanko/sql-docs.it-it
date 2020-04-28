---
title: Rimozione di SSMA per i componenti DB2 (DB2ToSQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060087"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Rimozione di SSMA per i componenti DB2 (DB2ToSQL)
Al termine della migrazione dei database da DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], potrebbe essere necessario disinstallare i componenti di SSMA. È possibile disinstallare i componenti client in qualsiasi momento. Tuttavia, non è consigliabile disinstallare il pacchetto di estensione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da a meno che i database migrati non usino più funzioni nello schema **ssma_DB2** del database **sysdb** .  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>Disinstallazione di SSMA per il client DB2  
È possibile disinstallare SSMA utilizzando **Installazione applicazioni**.  
  
**Per disinstallare SSMA**  
  
1.  Nel Pannello di controllo aprire **Programmi e funzionalità**.  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] Selezionare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per DB2**, quindi fare clic su **Rimuovi**.  
  
3.  Per confermare che si vuole disinstallare SSMA, fare clic su **Sì**.  
  
## <a name="uninstalling-the-extension-pack"></a>Disinstallazione del pacchetto di estensione  
Se si è certi che i database migrati non utilizzino oggetti nello schema **sysdb. ssma_DB2** , è possibile rimuovere il pacchetto di estensione eliminando tale pacchetto dallo schema. non è presente alcuna disinstallazione di Windows  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per il client DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Installazione dei componenti di SSMA in SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
