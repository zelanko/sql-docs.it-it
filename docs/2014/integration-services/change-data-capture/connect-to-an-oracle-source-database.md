---
title: Connettersi a un database di origine Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bf25496a36a1c5864ee4101226b6432663af111f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84923462"
---
# <a name="connect-to-an-oracle-source-database"></a>Connettersi a un database di origine Oracle
  Utilizzare la pagina Oracle Source per fornire le informazioni necessarie per la connessione al database di origine Oracle. Tramite l'istanza di CDC verranno letti i log di rollforward del database Oracle a cui si è effettuata la connessione.  
  
 **Oracle Connect String**  
 Immettere la stringa di connessione Oracle nel computer contenente il database Oracle in uso. La stringa di connessione viene scritta in uno dei modi seguenti:  
  
 `host[:port][/service name]`  
  
 Nella stringa di connessione è anche possibile specificare un descrittore della connessione di rete Oracle, ad esempio `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 Se si utilizza un server di elenchi in linea o nomi TNS, la stringa di connessione può essere il nome della connessione.  
  
 **Oracle Log Mining Authentication**  
 Per immettere le credenziali per l'utente del database Oracle autorizzato per il log mining, selezionare una delle opzioni seguenti:  
  
-   **Windows Authentication**: selezionare questa opzione per utilizzare le credenziali del dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: se si seleziona questa opzione, è necessario digitare il **nome utente** e la **password** dell'utente nel database Oracle a cui si effettua la connessione.  
  
> [!NOTE]
>  Per poter essere un utente del log mining un utente deve disporre dei privilegi seguenti per il database Oracle.  
> 
>  -   Seleziona su\<any-captured-table>  
> -   SELECT ANY TRANSACTION  
> -   EXECUTE on DBMS LOGMNR  
> -   SELECT on V$LOGMNR CONTENTS  
> -   SELECT on V$ARCHIVED LOG  
> -   SELECT on V$LOG  
> -   SELECT on V$LOGFILE  
> -   SELECT on V$DATABASE  
> -   SELECT on V$THREAD  
> -   SELECT on ALL INDEXES  
> -   SELECT on ALL OBJECTS  
> -   SELECT on DBA OBJECTS  
> -   SELECT on ALL TABLES  
> 
>  Se non è possibile concedere alcuni di questi privilegi a un V$xxx, concederli a V_S$xxx.  
  
 **Test connessione**  
 Fare clic su **Test connessione** per determinare se è stata stabilita una connessione al computer remoto in cui è presente il database Oracle. Una finestra di dialogo informerà l'utente se la connessione è stata stabilita correttamente.  
  
> [!IMPORTANT]  
>  A causa di un problema noto, la connessione al database di origine Oracle potrebbe non riuscire se la progettazione di CDC non viene eseguita con i privilegi di amministratore. Se la connessione non può essere stabilita, chiudere e riavviare la finestra di progettazione di CDC utilizzando l'opzione **Esegui come amministratore** .  
  
 Dopo avere completato l'immissione delle informazioni in questa pagina, scegliere **Avanti** in [Select Oracle Tables and Columns](select-oracle-tables-and-columns.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Modificare le proprietà dell'istanza](edit-instance-properties.md)  
  
  
