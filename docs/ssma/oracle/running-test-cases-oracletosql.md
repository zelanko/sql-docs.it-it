---
title: Esecuzione di Test case (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 537865967d0e43b7dd9501f9fbb7b9605f5b9367
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625794"
---
# <a name="running-test-cases-oracletosql"></a>Esecuzione di test case (OracleToSQL)
Quando si SSMA Tester esegue un Test Case, esegue gli oggetti selezionati per il test e viene creato un report sui risultati della verifica. Se i risultati sono identici in entrambe le piattaforme, il test ha esito positivo. La corrispondenza degli oggetti tra Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene determinato in base alle impostazioni di mapping dello schema per il progetto SSMA corrente.  
  
Un requisito necessario per un test ha esito positivo è che tutti gli oggetti Oracle vengono convertiti e caricati nel database di destinazione. Inoltre, i dati della tabella devono essere migrati in modo che il contenuto delle tabelle su entrambe le piattaforme siano sincronizzato.  
  
## <a name="run-test-case"></a>Eseguire Test Case  
Per l'esecuzione preparata Test Case:  
  
1.  Scegliere il **eseguire** pulsante.  
  
2.  Nel **Connetti a Oracle** della finestra di dialogo immettere le informazioni di connessione e quindi fare clic su **Connect**.  
  
Una volta completato il test, viene creato il Report di Test Case. Fare clic sui **Report** pulsante per visualizzare i [Report di Test Case](viewing-test-case-reports-oracletosql.md). Il risultato del test (Report del Test Case) viene automaticamente archiviato nel [Repository dei risultati del Test](using-test-repositories-oracletosql.md) per un uso successivo.  
  
## <a name="test-case-execution-steps"></a>Passaggi per l'esecuzione dei test Case  
  
### <a name="prerequisites"></a>Prerequisiti  
SSMA Tester controlla se vengono soddisfatti tutti i prerequisiti per l'esecuzione di test prima dell'inizio del test. Se non vengono soddisfatte determinate condizioni, viene visualizzato un messaggio di errore.  
  
### <a name="initialization"></a>Inizializzazione  
In questa fase, Tester di SSMA crea oggetti ausiliari (tabelle, trigger e viste) nello schema SSMATESTER_ORACLE del server Oracle. Consentono di tracciamento delle modifiche apportate in oggetti interessati scelti per la verifica.  
  
Si supponga che la tabella verificata è denominata USER_TABLE. Per una tabella, vengono creati i seguenti oggetti ausiliari in Oracle.  
  
||||  
|-|-|-|  
|Nome|Type|Descrizione|  
|USER_TABLE$Trg|trigger|Attivare il controllo delle modifiche nella tabella verificata.|  
|USER_TABLE$AUD|table|Tabella in cui vengono salvate le righe eliminate e sovrascritte.|  
|USER_TABLE$AUDID|table|Tabella in cui vengono salvate righe nuove e modificate.|  
|USER_TABLE|vista|Rappresentazione semplificata delle modifiche nella tabella.|  
|USER_TABLE$NEW|vista|Rappresentazione semplificata di righe inserite e sovrascritte.|  
|USER_TABLE$NEW_ID|vista|Identificazione di righe inserite e modificate.|  
|USER_TABLE$OLD|vista|Rappresentazione semplificata di righe eliminate e sovrascritte.|  
  
L'oggetto seguente viene creato nello schema di tabella verificata nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||||  
|-|-|-|  
|Nome|Type|Descrizione|  
|USER_TABLE$Trg|trigger|Attivare il controllo delle modifiche nella tabella verificata.|  
  
E gli oggetti seguenti vengono creati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nel database ssmatesterdb.  
  
||||  
|-|-|-|  
|Nome|Type|Descrizione|  
|USER_TABLE$Aud|table|Tabella in cui vengono salvate le righe eliminate e sovrascritte.|  
|USER_TABLE$AudID|table|Tabella in cui vengono salvate righe nuove e modificate.|  
|USER_TABLE|vista|Rappresentazione semplificata delle modifiche nella tabella.|  
|USER_TABLE$new|vista|Rappresentazione semplificata di righe inserite e sovrascritte.|  
|USER_TABLE$new_id|vista|Identificazione di righe inserite e modificate.|  
|USER_TABLE$old|vista|Rappresentazione semplificata di righe eliminate e sovrascritte.|  
  
### <a name="test-object-calls"></a>Chiamate a oggetti di test  
In questa fase, Tester di SSMA richiama ogni oggetto selezionato per la sperimentazione, vengono confrontati i risultati e Mostra il report.  
  
### <a name="finalization"></a>Finalizzazione  
Durante la finalizzazione SSMA Tester pulisce gli oggetti ausiliari creati nel **inizializzazione** passaggio.  
  
## <a name="next-step"></a>Passaggio successivo  
[Viewing Test Case Reports &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Selezione e configurazione degli oggetti da testare &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Selezione e configurazione degli oggetti interessati &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Test di oggetti di Database migrati &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
