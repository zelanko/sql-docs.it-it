---
title: Esecuzione di Test case (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 664c2d3d4e1a1cea78bd93c748d9c17d2f1fe670
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667721"
---
# <a name="running-test-cases-sybasetosql"></a>Esecuzione di test case (SybaseToSQL)
Quando si SSMA Tester esegue un Test Case, esegue gli oggetti selezionati per il test e viene creato un report sui risultati della verifica. Se i risultati sono identici in entrambe le piattaforme, il test ha esito positivo. La corrispondenza degli oggetti tra Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene determinato in base alle impostazioni di mapping dello schema per il progetto SSMA corrente.  
  
Un requisito necessario per un test ha esito positivo è che tutti gli oggetti di Sybase sono convertiti e caricati nel database di destinazione. Inoltre, i dati della tabella devono essere migrati in modo che il contenuto delle tabelle su entrambe le piattaforme siano sincronizzato.  
  
## <a name="run-test-case"></a>Eseguire Test Case  
Per l'esecuzione preparata Test Case:  
  
1.  Scegliere il **eseguire** pulsante.  
  
2.  Nel **connettersi a Sybase** della finestra di dialogo immettere le informazioni di connessione e quindi fare clic su **Connect**.  
  
Una volta completato il test, viene creato il Report di Test Case. Fare clic sui **Report** pulsante per visualizzare i [visualizzazione di report di Test Case &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). Il risultato del test (Report del Test Case) viene automaticamente archiviato nel [usando i repository di Test &#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) per un uso successivo.  
  
## <a name="test-case-execution-steps"></a>Passaggi per l'esecuzione dei test Case  
  
### <a name="prerequisites"></a>Prerequisiti  
SSMA Tester controlla se vengono soddisfatti tutti i prerequisiti per l'esecuzione di test prima dell'inizio del test. Se non vengono soddisfatte determinate condizioni, viene visualizzato un messaggio di errore.  
  
### <a name="initialization"></a>Inizializzazione  
In questa fase, Tester di SSMA crea ausiliari oggetti (tabelle, trigger e viste) sia di Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Consentono di tracciamento delle modifiche apportate nelle tabelle interessate scelte per la verifica se la modalità tabella confronti **solo le modifiche**.  
  
Si supponga che la tabella verificata è denominata USER_TABLE. Per una tabella, vengono creati i seguenti oggetti ausiliari in Sybase.  
  
I seguenti oggetti vengono creati Sybase nel database SSMATESTER2005db o SSMATESTER2008db e a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database ssmatesterdb_syb.  
  
|Nome|Type|Descrizione|  
|--------|--------|---------------|  
|USER_TABLE$Trg|Trigger|Attivare il controllo delle modifiche nella tabella verificata.|  
|USER_TABLE$Aud|Tabella|Tabella in cui vengono salvate le righe eliminate e sovrascritte.|  
|USER_TABLE$AudID|Tabella|Tabella in cui vengono salvate righe nuove e modificate.|  
|USER_TABLE|visualizzazione|Rappresentazione semplificata delle modifiche nella tabella.|  
|USER_TABLE$new|visualizzazione|Rappresentazione semplificata di righe inserite e sovrascritte.|  
|USER_TABLE$new_id|visualizzazione|Identificazione di righe inserite e modificate.|  
|USER_TABLE$old|visualizzazione|Rappresentazione semplificata di righe eliminate e sovrascritte.|  
  
L'oggetto seguente viene creato nel database della tabella verificato Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome|Type|Descrizione|  
|--------|--------|---------------|  
|USER_TABLE$Trg|Trigger|Attivare il controllo delle modifiche nella tabella verificata.|  
  
### <a name="test-object-calls"></a>Chiamate a oggetti di test  
In questa fase, Tester di SSMA richiama ogni oggetto selezionato per la sperimentazione, vengono confrontati i risultati e Mostra il report.  
  
### <a name="finalization"></a>Finalizzazione  
Durante la finalizzazione SSMA Tester pulisce gli oggetti ausiliari creati nel **inizializzazione** passaggio.  
  
## <a name="next-step"></a>Passaggio successivo  
[Visualizzazione dei report di Test Case &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Selezione e configurazione degli oggetti da testare &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Selezione e configurazione degli oggetti interessati &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Test di oggetti di Database migrati &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
