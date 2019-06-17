---
title: Configurare l'opzione di configurazione del server network packet size | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default packet size
- size [SQL Server], packets
- packets [SQL Server], size
- network packet size option
ms.assetid: 236985bf-fc4a-4a57-98f7-a71ef977fd7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4bd992f16158e7286db668256dc5963d83dbd4b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787000"
---
# <a name="configure-the-network-packet-size-server-configuration-option"></a>Configurare l'opzione di configurazione del server network packet size
  In questo argomento viene descritto come configurare il `network packet size` opzione di configurazione del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il `network packet size` opzione consente di impostare le dimensioni del pacchetto (in byte) che viene usata in tutta la rete. I pacchetti sono i blocchi di dati di dimensioni fisse utilizzati per il trasferimento delle richieste e delle risposte tra client e server. Le dimensioni predefinite del pacchetto sono di 4.096 byte.  
  
> [!NOTE]  
>  È consigliabile modificare le dimensioni dei pacchetti solo se si è certi che l'operazione determinerà un miglioramento delle prestazioni. Per la maggior parte delle applicazioni, le dimensioni predefinite risultano ottimali.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione network packet size tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo aver configurato l'opzione network packet size](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Il valore massimo consentito per network packet size per le connessioni crittografate è di 16.383 byte.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se in un'applicazione vengono eseguite operazioni di copia bulk o inviate e ricevute quantità elevate di dati text o image, l'utilizzo di pacchetti di dimensioni maggiori rispetto a quelle predefinite potrebbe determinare un miglioramento delle prestazioni, poiché viene ridotto il numero di operazioni di lettura e scrittura di rete. Se in un'applicazione vengono inviate e ricevute quantità limitate di dati, è possibile impostare le dimensioni del pacchetto su 512 byte, un valore sufficiente per la maggior parte dei trasferimenti di dati.  
  
-   Nei sistemi che usano protocolli di rete diversi, è consigliabile impostare le dimensioni pacchetto di rete corrispondenti al protocollo usato più di frequente. L'opzione network packet size determina un miglioramento delle prestazioni della rete se i protocolli di rete supportano pacchetti di dimensioni maggiori. Le applicazioni client possono modificare tale valore.  
  
-   È inoltre possibile richiedere di modificare le dimensioni dei pacchetti tramite le funzioni OLE DB, ODBC (Open Database Connectivity) e DB-Library. Se il server non supporta le dimensioni del pacchetto richieste, un messaggio di avviso verrà inviato al client da [!INCLUDE[ssDE](../../includes/ssde-md.md)] . In alcuni casi la modifica delle dimensioni dei pacchetti potrebbe provocare un errore del collegamento di comunicazione, ad esempio:  
  
     `Native Error: 233, no process is on the other end of the pipe.`  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Per configurare l'opzione network packet size  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  In **Rete**selezionare un valore per la casella **Dimensioni pacchetto di rete** .  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Per configurare l'opzione network packet size  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `network packet size` su `6500` byte.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'network packet size', 6500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo aver configurato l'opzione network packet size  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
