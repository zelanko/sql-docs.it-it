---
title: Visualizzazione di un log di controllo di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fa30824e32faae5feee1612305c1ca292d44e8e4
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100166"
---
# <a name="view-a-sql-server-audit-log"></a>Visualizzazione di un log di controllo di SQL Server
  Questo argomento descrive come visualizzare un log di controllo di SQL Server in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare un log di controllo di SQL Server mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessaria l'autorizzazione `CONTROL SERVER`.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Per visualizzare un log di controllo di SQL Server  
  
1.  In Esplora oggetti espandere la cartella **Sicurezza** .  
  
2.  Espandere la cartella **Controlli** .  
  
3.  Fare clic con il pulsante destro del mouse sul log di controllo da visualizzare e selezionare **Visualizza log di controllo**. Verrà visualizzata la **Visualizzatore File di Log -**_nome_server_ nella finestra di dialogo. Per altre informazioni, vedere [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md).  
  
4.  Al termine, fare clic su **Chiudi**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] consiglia di visualizzare il log di controllo usando il Visualizzatore file di log. Tuttavia, se si sta creando un sistema di monitoraggio automatizzato, è possibile leggere direttamente le informazioni nel file di controllo usando la funzione [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql). La lettura diretta del file restituisce i dati in un formato leggermente diverso (non elaborato). Vedere **sys.fn_get_audit_file** per altre informazioni  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Audit &#40;Database Engine&#41;](sql-server-audit-database-engine.md)   
 [Scrittura di eventi di controllo di SQL Server nel registro di sicurezza](write-sql-server-audit-events-to-the-security-log.md)  
  
  
