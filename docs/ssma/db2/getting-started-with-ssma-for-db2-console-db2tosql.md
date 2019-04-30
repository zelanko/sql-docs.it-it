---
title: Introduzione a SSMA per DB2 Console (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3b8417d75ab0a08532dd073b3ce7f803b3f7490c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453321"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Introduzione a SSMA per DB2 Console (DB2ToSQL)
In questa sezione viene descritta la procedura per avviare e iniziare a usare l'applicazione console di DB2. Anche nell'elenco, nel presente documento, vengono utilizzate le convenzioni di in una finestra di output della Console SSMA tipica.  
  
## <a name="launching-ssma-console"></a>Avviare Console SSMA  
Per avviare l'applicazione console SSMA, procedere come segue:  
  
1.  Passare a **avviare** e scegliere **tutti i programmi**.  
  
2.  Scegliere il  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per DB2 Prompt dei comandi** scelta rapida.  
  
    Viene visualizzato il menu di utilizzo della Console SSMA e `(/? Help)`, che consentono di iniziare a usare l'applicazione console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedure per l'utilizzo della Console SSMA  
Dopo che la console viene avviata correttamente nel sistema Windows, è possibile utilizzare i passaggi seguenti per risolverlo:  
  
1.  Configurare Console SSMA tramite i file di script. Per altre informazioni su questa sezione, vedere [creazione di file di Script &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md) .  
  
2.  [Creazione di file di valore della variabile &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [Creazione di file di connessione del Server &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [Esecuzione della Console SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) secondo le esigenze di progetto  
  
Altre funzionalità:  
  
1.  [La gestione delle password](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) ed esportare / importare in un altro computer della finestra  
  
2.  [Generazione di report](https://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883) per visualizzare il codice xml dettagliate dell'output di report per la migrazione di dati e /conversion assessment. I report di errore dettagliati possono anche essere generati per i comandi di aggiornamento e la sincronizzazione.  
  
## <a name="ssma-console-output-conventions"></a>Convenzioni di Output di Console SSMA  
Dopo l'esecuzione di comandi di script SSMA e le opzioni, il programma di console vengono visualizzati i risultati e messaggi (le informazioni, errore, e così via) per l'utente nella console o se necessario, reindirizza a un file di output xml. Ogni tipo di messaggio nell'output è identificato da un colore univoco. Ad esempio, il messaggio di testo di colore bianco indica i comandi di file di script; quello di colore verde rappresenta un prompt dei comandi per l'input utente e così via.  
  
![Ssmaconsoleoutput_oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "ssmaconsoleoutput_oracle")  
  
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
[Installazione di SSMA per DB2](https://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
