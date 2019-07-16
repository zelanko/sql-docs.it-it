---
title: Introduzione a SSMA per Sybase Console (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029115"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Introduzione a SSMA per Sybase Console (SybaseToSQL)
In questa sezione viene descritta la procedura per l'avvio e Introduzione a SSMA per Sybase applicazione di console. Anche elencati nel presente documento vengono utilizzate le convenzioni di in una finestra di output della Console SSMA tipica.  
  
## <a name="launching-the-ssma-console"></a>L'avvio della Console SSMA  
Per avviare l'applicazione console SSMA, procedere come segue:  
  
1.  Andare a Start e quindi scegliere tutti i programmi.  
  
2.  Scegliere il **SQL Server Migration Assistant per Sybase Prompt dei comandi** scelta rapida.  
  
    Viene visualizzato il menu di utilizzo della Console SSMA e `(/? Help)`, che consentono di iniziare a usare l'applicazione console.  
  
## <a name="using-the-ssma-console"></a>Utilizzo della Console SSMA  
Dopo che la console viene avviata correttamente nel sistema Windows, è possibile utilizzare i passaggi seguenti per lavorare su di esso:  
  
1.  Configurare Console SSMA tramite i file di script. Per altre informazioni su questa sezione, vedere [creazione di file di Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Creazione di file di valore della variabile &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Creazione di file di connessione del Server &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Esecuzione della Console SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) secondo le esigenze di progetto. 
  
Altre funzionalità:  
  
1.  [Specificare una password](managing-passwords-sybasetosql.md) e importazione/esportazione, in altri computer della finestra.  
  
2.  [Generare report](generating-reports-sybasetosql.md) per visualizzare il codice xml dettagliati report per la migrazione di conversione o di valutazione e i dati di output. È anche possibile generare i report dettagliato degli errori per i comandi di aggiornamento e la sincronizzazione.  
  
## <a name="ssma-console-output-conventions"></a>Convenzioni di output di Console SSMA  
Dopo l'esecuzione di comandi di script SSMA e le opzioni, il programma di console vengono visualizzati i risultati e messaggi (le informazioni, errore, e così via) per l'utente nella console o, se necessario, reindirizza a un file di output xml. Ogni tipo di messaggio nell'output è identificato da un colore univoco. Ad esempio, il messaggio di testo di colore bianco indica i comandi di file di script; quello di colore verde rappresenta un prompt dei comandi per l'input utente e così via.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Colore dall'interpretazione dell'output della console viene visualizzato nella tabella seguente:  
  
|Colore|Descrizione|  
|---------|---------------|  
|Rosso|Errore irreversibile durante l'esecuzione|  
|Grigio|Data e un timestamp, messaggio all'utente|  
|Bianco|Comandi di file di script, il tipo di messaggio|  
|Giallo|Avviso|  
|Green|Richiedi input utente|  
|azzurro|Inizio, fine e risultati di un'operazione|  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
