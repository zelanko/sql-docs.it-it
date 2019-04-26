---
title: Test migrati (OracleToSQL) gli oggetti di Database | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 771e9a4553679ae2afa0dd58d83b1d15ccf0fd62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626058"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>Test di oggetti di database migrati (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Oracle Tester (SSMA Tester) verifica automaticamente la conversione di oggetti di database e la migrazione dei dati apportate da SSMA. Al termine di tutti i passaggi di migrazione di SSMA, utilizzare il Tester di SSMA per verificare che gli oggetti convertiti funzionano allo stesso modo e che tutti i dati è stato trasferito correttamente.  
  
È possibile testare i seguenti tipi di oggetto con SSMA Tester:  
  
-   Tabelle  
  
-   Stored procedure, incluse quelle nel pacchetto.  
  
-   Funzioni definite dall'utente, incluse le funzioni nel pacchetto.  
  
-   Visualizzazioni.  
  
-   Istruzioni autonome.  
  
SSMA Tester esegue gli oggetti selezionati per il testing in Oracle e le relative controparti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Successivamente, confronta i risultati in base ai criteri seguenti:  
  
-   Le modifiche nei dati di tabella sono identici?  
  
-   Sono i valori dei parametri di output per le procedure e le funzioni identiche?  
  
-   Le funzioni restituiscono gli stessi risultati?  
  
-   Sono che i set di risultati identici?  
  
> [!NOTE]  
> Attenzione! Non utilizzare mai SSMA Tester nei sistemi di produzione. Durante l'esecuzione di Tester lo schema di origine e i dati vengono modificati. Nel frattempo, al ripristino completo dello stato originale potrebbe essere impossibile per alcuni tipi di codice testato.  
  
## <a name="prerequisites"></a>Prerequisiti  
Se si desidera utilizzare Tester SSMA, installare SSMA Oracle Extension Pack con le **installare Database Tester** opzione impostata su on.  
  
Per consentire il confronto dei dati della tabella risultante, impostare il **colonna generare ROWID** possibilità **Yes** prima che inizi la conversione dello schema. SSMA verrà aggiunta una colonna ROWID a tutte le tabelle durante l'esecuzione del **convertire lo Schema** comando.  
  
Inoltre, verificare quanto segue:  
  
-   Vengono installati gli strumenti client Oracle nel computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito.  
  
-   Integrazione con Common Language Runtime (CLR) è stato attivato il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di Database.  
  
Si noti che la versione corrente di SSMA Tester non supporta l'esecuzione parallela da utenti diversi nello stesso server di origine o destinazione.  
  
## <a name="getting-started"></a>Introduzione  
[Creazione di Test case &#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di componenti SSMA in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Le impostazioni di progetto &#40;conversione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
