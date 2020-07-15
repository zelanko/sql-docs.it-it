---
title: Visualizzazione di un log di controllo di SQL Server | Microsoft Docs
description: Informazioni su come visualizzare un log di controllo di SQL Server in SQL Server usando SQL Server Management Studio o Transact-SQL. La visualizzazione richiede l'autorizzazione CONTROL SERVER.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
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
ms.openlocfilehash: 02ed692b38f37c5818f7e8a24e5abf32ab1a186a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85884931"
---
# <a name="view-a-sql-server-audit-log"></a>Visualizzazione di un log di controllo di SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Questo argomento descrive come visualizzare un log di controllo di SQL Server in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare un log di controllo di SQL Server mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione **CONTROL SERVER** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Per visualizzare un log di controllo di SQL Server  
  
1.  In Esplora oggetti espandere la cartella **Sicurezza** .  
  
2.  Espandere la cartella **Controlli** .  
  
3.  Fare clic con il pulsante destro del mouse sul log di controllo da visualizzare e selezionare **Visualizza log di controllo**. Verrà visualizzata la finestra di dialogo **Visualizzatore file di log -** _nome\_server_. Per altre informazioni, vedere [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
4.  Al termine, fare clic su **Chiudi**.  

 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] consiglia di visualizzare il log di controllo usando il Visualizzatore file di log. Tuttavia, se si sta creando un sistema di monitoraggio automatizzato, è possibile leggere direttamente le informazioni nel file di controllo usando la funzione [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). La lettura diretta del file restituisce i dati in un formato leggermente diverso (non elaborato). Per altre informazioni, vedere **sys.fn_get_audit_file** .  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Scrittura di eventi di controllo di SQL Server nel registro di sicurezza](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
