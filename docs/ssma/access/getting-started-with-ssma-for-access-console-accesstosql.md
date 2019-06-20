---
title: Introduzione a SSMA per la Console di accesso (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 44e89e7c6ab10df13927247222e1f8564500fb8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759885"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Introduzione a SSMA per la Console di accesso (AccessToSQL)
In questa sezione viene descritta la procedura per avviare e iniziare a usare l'applicazione console di accesso. Anche nell'elenco, nel presente documento, vengono utilizzate le convenzioni di in una finestra di output della Console SSMA tipica.  
  
## <a name="launching-ssma-console"></a>Avviare Console SSMA  
Per avviare l'applicazione console SSMA, procedere come segue:  
  
1.  Passare a **avviare** e scegliere **tutti i programmi**.  
  
2.  Scegliere il **SQL Server Migration Assistant per Access Prompt dei comandi** scelta rapida.  
  
    Viene visualizzato il menu di utilizzo della Console SSMA e `(/? Help)`, che consentono di iniziare a usare l'applicazione console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedure per l'utilizzo della Console SSMA  
Dopo che la console viene avviata correttamente nel sistema Windows, è possibile utilizzare i passaggi seguenti per risolverlo:  
  
1.  Configurare Console SSMA tramite i file di script. Per altre informazioni su questa sezione, vedere [creazione di file di Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Creazione di file di valore della variabile &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Creazione di file di connessione del Server &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Esecuzione della Console SSMA &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) secondo le esigenze di progetto  
  
Altre funzionalità:  
  
1.  [Specificare una password](managing-passwords-accesstosql.md) ed esportare / importare in un altro computer della finestra  
  
2.  [Generare report](generating-reports-accesstosql.md) per visualizzare il codice xml dettagliate dell'output di report per la migrazione di dati e /conversion assessment. I report di errore dettagliati possono anche essere generati per i comandi di aggiornamento e la sincronizzazione.  
  
## <a name="ssma-console-output-conventions"></a>Convenzioni di Output di Console SSMA  
Dopo l'esecuzione di comandi di script SSMA e le opzioni, il programma di console vengono visualizzati i risultati e messaggi (le informazioni, errore, e così via) per l'utente nella console o se necessario, reindirizza a un file di output xml. Ogni tipo di messaggio nell'output è identificato da un colore univoco. Ad esempio, il messaggio di testo di colore bianco indica i comandi di file di script; quello di colore verde rappresenta un prompt dei comandi per l'input utente e così via.  
  
![Output della Console SSMA](../../ssma/access/media/ssmaconsoleoutput.jpg "Output della Console SSMA")  
  
Colore dall'interpretazione dell'output della console nella tabella seguente:  
  
|Colore|Descrizione|  
|---------|---------------|  
|Red|Errore irreversibile durante l'esecuzione|  
|Grigio|Data e un timestamp, messaggio all'utente|  
|Bianco|Comandi di file di script, il tipo di messaggio|  
|Giallo|Avviso|  
|Green|Richiedi input utente|  
|azzurro|Inizio, fine e il risultato di un'operazione|  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SQL Server Migration Assistant per Access](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
